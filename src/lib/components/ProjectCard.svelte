<script lang="ts">
	import { T, useLoader } from '@threlte/core';
	import { Canvas } from '@threlte/core';
	import { useTexture, OrbitControls, useProgress, transitions } from '@threlte/extras';
	import ProjectScene from './ProjectScene.svelte';
	import { tweened } from 'svelte/motion';
	import { fade } from 'svelte/transition';
	import { expoInOut, expoOut } from 'svelte/easing';

	const { progress } = useProgress();
	const tweenedProgress = tweened($progress, {
		duration: 1700
	});
	$: tweenedProgress.set($progress);
</script>

<article>
	<h1>Noise Cancel</h1>
	<div class="container">
		{#if $tweenedProgress < 1}
			<div
				transition:fade|local={{
					duration: 200,
					easing: expoInOut
				}}
				class="wrapper"
			>
				<p class="loading">Welcome to my Creative Friday</p>
				<div class="bar-wrapper">
					<div class="bar" style="width: {$tweenedProgress * 100}%" />
				</div>
			</div>
		{/if}
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
		font-size: clamp(2rem, 4vw, 5rem);
		white-space: nowrap;
		text-align: center;
		text-transform: uppercase;
		padding: 0;
		margin: 0;
	}

	.container {
		width: 100%;
		height: 100%;
		max-width: 100%;
		height: 100lvh;
		margin-left: auto;
	}

	.loading {
		font-size: 1.5rem;
		line-height: 1.25rem;
	}
	.wrapper {
		position: absolute;
		width: 100%;
		height: 100%;
		top: 0;
		left: 0;
		background-color: #eaf9d9;
		display: flex;
		flex-direction: column;
		gap: 0.25rem;
		align-items: center;
		justify-content: center;
		color: black;
	}
	.bar-wrapper {
		width: 33.333333%;
		height: 10px;
		border: 1px solid black;
		position: relative;
	}
	.bar {
		height: 100%;
		background-color: black;
	}
</style>
