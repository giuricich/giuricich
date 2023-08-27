<script lang="ts">
	import { text } from '@sveltejs/kit';
	import TextShadowProps from './TextShadowProps.svelte';

	let textShadowData = {
		offsetX: 0,
		offsetY: 0,
		blurRadius: 0,
		color: '#fff'
	};

	$: textShadow = `
        ${textShadowData.offsetX}px
        ${textShadowData.offsetY}px
        ${textShadowData.blurRadius}px
        ${textShadowData.color}
    `;
	$: paragraphStyle = `
        text-shadow: ${textShadow};`;
</script>

<svelte:head>
	<title>0px</title>
</svelte:head>

<div class="dots" />
<section>
	<div class="name">
		<h1>Isaac Giuricich</h1>
		<br />
		<p>カタカナ</p>
	</div>

	<div class="name name2">
		<h1>Isaac Giuricich</h1>
		<br />
		<p>カタカナ</p>
	</div>
	<div class="text">
		<p>{textShadow}</p>
	</div>
	<TextShadowProps bind:data={textShadowData} />
</section>

<style>
	@import url('reset.css');

	:global(body) {
		/* background: url("/images/dots.png"); */
		background-color: black;
		background-size: cover;
		image-rendering: pixelated;
		image-rendering: crisp-edges;
		background-repeat: no-repeat;
		/* height: 200vh; */
	}
	.dots {
		width: 100%;
		height: 200lvh;
		background: url('/images/dots.png');
		position: absolute;
		background-size: cover;
		image-rendering: pixelated;
		image-rendering: crisp-edges;
		background-repeat: no-repeat;
		z-index: 1;
		pointer-events: none;
		/* transition: all 100ms ease-out; */
		filter: blur(10px);
	}
	.dots:hover {
		/* filter: blur(0); */
	}
	section {
		height: 100%;
		width: 100%;
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
	}
	.name {
		width: max-content;
		position: fixed;
		top: 0rem;
		left: 0;
		transform: rotate(-50deg) translate(-80%, 100%);
		transition: all 100ms ease-out;
		filter: blur(2px);
	}
	.name2 {
		transform: rotate(-50deg) translate(20%, 100%);
	}
	.name > h1,
	.name > p {
		max-width: fit-content;
	}
	.name:hover {
		/* text-shadow: 0 0 8px #ee28ca; */
		filter: drop-shadow(0 0 8px #ee28ca);
		/* filter: blur(0); */
		z-index: 2;
	}
	.name::before {
		content: '';
		z-index: -1;
		position: absolute;
		top: 0;
		right: 0;
		bottom: 0;
		left: 0;
		background: linear-gradient(0deg, #f4cef0 -91%, #844660 200%);
		transform: translate3d(0px, 0px, 0) scale(1);
		filter: blur(30px);
		opacity: 0.73;
		transition: opacity 0.3s;
		border-radius: inherit;
	}

	.name::after {
		content: '';
		z-index: -1;
		position: absolute;
		top: 0;
		right: 0;
		bottom: 0;
		left: 0;
		background: inherit;
		border-radius: inherit;
	}

	h1,
	p {
		font-family: serif;
		/* font-weight: ; */
		font-size: 3rem;
		text-rendering: auto;
		color: #fff;
		/* text-shadow: 0 0 5px #fff; */
		text-shadow: inherit;
		/* background-color: black; */
		border-radius: 12px;
	}
	.japanese {
		font-family: 'Yu Gothic';
		font-size: 3rem;
		text-rendering: auto;
		color: #fff;
		/* text-shadow: 0 0 5px #fff;
        background-color: black; */
		border-radius: 12px;
		writing-mode: vertical-rl;
	}
</style>
