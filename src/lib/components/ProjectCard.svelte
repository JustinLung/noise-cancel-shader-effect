<script lang="ts">
	import { T, useLoader } from '@threlte/core';
	import { Canvas } from '@threlte/core';
	import { useTexture, OrbitControls } from '@threlte/extras';
	import ProjectScene from './ProjectScene.svelte';
</script>

<article>
	<h1>Noise Cancel</h1>
	<div class="img-container">
		<Canvas>
			<ProjectScene />
		</Canvas>
	</div>
</article>

<style>
	article {
		display: flex;
		flex-direction: column;
		width: 100%;
		position: relative;
		margin: 0 auto;
	}

	h1 {
		position: absolute;
		top: 50%;
		left: 50%;
		transform: translate(-50%, -50%);
		color: #ffff;
		font-family: Arial, Helvetica, sans-serif;
		font-size: clamp(2rem, 4vw, 5rem);
		white-space: nowrap;
		text-align: center;
		text-transform: uppercase;
		padding: 0;
		margin: 0;
	}

	.img-container {
		width: 100%;
		height: 100%;
		max-width: 100%;
		height: 100lvh;
		margin-left: auto;
	}
</style>
