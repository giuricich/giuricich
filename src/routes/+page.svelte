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

	let styles = {
		'shadow': '0 0 1px black',
		'many-shadows': '0 0 1px black,',
		'cool-filter' : 'drop-shadow(-1px -1px 0 red) drop-shadow(1px 1px 0 blue)',
		'invert-filter' : 'drop-shadow(-1px -1px 0 cyan) drop-shadow(1px 1px 0 yellow)'
	};

	styles['many-shadows'] = styles['many-shadows'].repeat(4).slice(0, -1);

	$: cssVarStyles = Object.entries(styles)
		.map(([key, value]) => `--${key}:${value}`)
		.join(';');

	const pixels = '2px';
</script>

<svelte:head>
	<title>0px</title>
</svelte:head>

<div class="dots" />
<section style="{cssVarStyles}">
	<div class="name">
		<h1>Isaac Giuricich</h1>
		<!-- <p>カタカナ</p> -->
	</div>

	<div class="name name2">
		<h1>Isaac Giuricich</h1>
		<!-- <p>カタカナ</p> -->
	</div>
	<div class="about">
		<!-- <p class="japanese">イサク・ジュリシッチ</p> -->
		<p>i am from canada</p>
		<p>i make websites</p>
		<p><em>i wish i were a bird</em></p>

	</div>

	<!-- <div class="text">
		<p>{textShadow}</p>
	</div> -->
	<!-- <TextShadowProps bind:data={textShadowData} /> -->
</section>

<style>
	@import url('reset.css');
	@font-face {
		font-family: "PP Mondwest Bold";
		src: url("/PPMondwest-Bold.woff") format("woff")
	}

	section {
		/* tall screens ONLY */
		max-height: 100vh;

		/* square and wide screens */

		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
		height: 100rem;
		min-height: 100vh;
		position: relative;

		/* filter: var(--cool-filter); */
	}
	section::before {
	/* dots */
		content: '';
		position: absolute;
		top: 0;
		left: 0;
		width: 100vw;
		height: 100rem;
		min-height: 100vh;

		

		background: url('/images/dots.png');
		background-size: cover;
		image-rendering: pixelated;
		image-rendering: crisp-edges;
		background-repeat: no-repeat;
		filter: var(--cool-filter);
	}
	.about {
		font-size: 9vw;
		position: absolute;
		width: 10rem;
		/* height: 60vh; */
		bottom: 1rem;
		right: 1rem;
		width: max-content;
		display: flex;
		flex-direction: column;
		border: 1px solid white;
		background: black;
		padding: 1rem;
	}
	.name {
		/* tall styles */
		font-size: 11vw;

		/* square and wide styles */
		width: max-content;
		word-wrap: none;
		white-space: nowrap;
		position: absolute;
		top: 0rem;
		left: 0;
		transform: rotate(-50deg) translate(-80%, 100%);
		transition: all 100ms ease-out;
		overflow: hidden;
		background: black;
	}
	.name2 {
		transform: rotate(-50deg) translate(20%, 100%);
	}
	.name > h1,
	.name > p {
		max-width: fit-content;
	}
	.name:hover {
		/* z-index: 2; */
		/* filter: var(--cool-filter); */
	}
	h1 {
		font-weight: bold;
	}

	h1,
	p {
		font-family: 'PP Mondwest Bold';
		font-size: inherit;
		/* font-weight: 100; */
		color: white;
		text-rendering: optimizeLegibility;
		/* background-color: #000; */
		image-rendering: pixelated;
		filter: var(--cool-filter);

	}
	.japanese {
		font-family: 'Yu Gothic';
		font-size: 3rem;
		text-rendering: auto;
		color: #fff;
		text-shadow: 0 0 5px #fff;
        background-color: black;
		border-radius: 12px;
		writing-mode: vertical-rl;
	}
	
	/* write a media query that applys styles to desktop screens */
	@media (min-width: 1024px) {
		:global(body) {
			max-height: initial;
			height: 200vh;
			overflow-y: auto !important;
		}
		section {
			height: 200vh;
			max-height: 200vh;
			/* position: relative; */
		}
		section::before {
			height: 200vh;
		}
		.about {
			height: auto !important;
			/* position: absolute; */
		}
	}


		/* make an alternate version of the site with a white background */
		/* trust me it looks suoer cool */
	@media(prefers-color-scheme: light) {
		:global(body) {
			background-color: white !important;
			filter: invert(1);
		}
		h1, p {
			background: none !important;
			/* text-shadow: 0 0 5px black; */
			/* color: black; */
			/* filter: var(--invert-filter); */
		}
		.about {
			/* border: 1px solid black; */
			/* background: none; */
			/* this is for when i figure out how to make the bubbles black */
			/* background: white; */
		}
		.name {

			/* this is for when i figure out how to make the bubbles black */
			/* background: black; */
		}
		section::before {
			/* filter: invert(1); */
			/* filter: var(--invert-filter); */
		}
	}

	:global(body) {
		background-color: black;
		background-size: cover;
		image-rendering: pixelated;
		image-rendering: crisp-edges;
		background-repeat: no-repeat;
		overflow-x: hidden;
		/* cool case where overflow-y actually effects */
		/* (its the name that overflowing on the btm)  */
		overflow-y: hidden;
		/* tall screens ONLY */
		max-height: 100vh;
	}
</style>
