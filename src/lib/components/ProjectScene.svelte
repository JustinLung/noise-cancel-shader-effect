<script lang="ts">
	import { T, useFrame } from '@threlte/core';
	import { Canvas } from '@threlte/core';
	import { useTexture, OrbitControls, Center } from '@threlte/extras';
	import ProjectScene from './ProjectScene.svelte';
	import vertexShader from '$lib/shaders/vertex.glsl?raw';
	import fragmentShader from '$lib/shaders/fragment.glsl?raw';
	import { Vector2 } from 'three';
	import { BufferAttribute } from 'three';

	const map = useTexture('/images/project.png');

	let rotation = 0;
	useFrame((state, delta) => {
		rotation += delta;
	});
</script>

<T.PerspectiveCamera makeDefault position={[0, 0, 15]}>
	<!-- <OrbitControls /> -->
</T.PerspectiveCamera>

{#await map then value}
	<Center>
		<T.Mesh rotation.y={rotation}>
			<T.TorusKnotGeometry
				on:create={({ ref }) => {
					console.log(ref);
					const count = ref.attributes.position.count;
					const randoms = new Float32Array(count);
					for (let i = 0; i < count; i++) {
						randoms[i] = Math.random();
					}
					ref.setAttribute('aRandom', new BufferAttribute(randoms, 1));
				}}
			/>
			<T.ShaderMaterial
				{vertexShader}
				{fragmentShader}
				wireframes={false}
				uniforms={{
					uFrequency: {
						value: new Vector2(10, 6)
					},
					uTime: {
						value: 0
					}
				}}
			/>
		</T.Mesh>
	</Center>
{/await}
