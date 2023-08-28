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
		'cool-filter' : 'drop-shadow(-1px -1px 0 red) drop-shadow(1px 1px 0 blue)'
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
		<br />
		<!-- <p>カタカナ</p> -->
	</div>

	<div class="name name2">
		<h1>Isaac Giuricich</h1>
		<br />
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

	:global(body) {
		/* background: url("/images/dots.png"); */
		background-color: black;
		background-size: cover;
		image-rendering: pixelated;
		image-rendering: crisp-edges;
		background-repeat: no-repeat;
		/* height: 200vh; */
	}
	section {
		height: 100%;
		width: 100%;
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
		/* filter: var(--cool-filter); */
	}
	section::before {
		content: '';
		position: absolute;
		top: 0;
		left: 0;
		width: 100%;
		height: 200vh;
		background: url('/images/dots.png');
		background-size: cover;
		image-rendering: pixelated;
		image-rendering: crisp-edges;
		background-repeat: no-repeat;
		filter: var(--cool-filter);
		/* filter: blur(10px); */
	}
	.name {
		width: max-content;
		position: absolute;
		top: 0rem;
		left: 0;
		transform: rotate(-50deg) translate(-80%, 100%);
		transition: all 100ms ease-out;
		/* filter: blur(2px); */
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
		/* filter: drop-shadow(0 0 8px #ee28ca); */
		/* filter: blur(0); */
		z-index: 2;
		filter: var(--cool-filter);
	}

	h1,
	p {
		font-family: 'PP Mondwest';
		font-size: 10rem;
		color: white;
		/* text-shadow: var(--many-shadows) ; */
		/* text-shadow: 0 0 5px white; */
		/* text-shadow: inherit; */
		background-color: #000;
		/* border-radius: 12px; */
		/* line-height: 30px; */
		image-rendering: pixelated;
		/* line-height: 0; */
		/* border-top: 6rem solid black;
		border-bottom: 6rem solid black; */
		/* border: 1px solid black; */

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
	.about {
		position: absolute;
		top: 110vh;
		right: 5px;
		width: max-content;
		display: flex;
		flex-direction: column;
		/* border: 1px solid white; */
		background: black;
		padding: 16px;
	}
</style>
