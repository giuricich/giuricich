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
		shadow: '0 0 1px black',
		'many-shadows': '0 0 1px black,',
		'cool-filter': 'drop-shadow(-.1vw -.1vw 0 red) drop-shadow(.1vw .1vw 0 blue)',
		'invert-filter': 'drop-shadow(-.1vw -.1vw 0 cyan) drop-shadow(.1vw .1vw 0 yellow)'
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
<section style={cssVarStyles}>
	<div class="name">
		<h1>Isaac GiuricichIsaac GiuricichIsaac Giuricich</h1>
	</div>

	<div class="boxes">
		<div class="box about">
			<p>i am from canada</p>
			<p>i make websites</p>
			<p><em>i wish i were a bird</em></p>
		</div>
		<div class="box showcase">
			<p>i do <em>not</em> play undertale</p>
		</div>
		<div class="box contact">
			<p>checkout my:</p>
			<p>github</p>
			<p>linkedin</p>
			<p>email</p>
			<p>isaac@giuricich.ca</p>
		</div>
	</div>
</section>

<style>
	@import url('reset.css');
	@font-face {
		font-family: 'PP Mondwest Bold';
		src: url('/PPMondwest-Bold.woff') format('woff');
	}

	section {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
		position: relative;
		/* for name text overflow */
		width: 100%;
		overflow: hidden;
	}
	section::before {
		/* dots */
		content: '';
		position: absolute;
		top: 0;
		left: 0;
		width: 100vw;
		height: 100%;

		background: url('/images/dots.png');
		background-repeat: no-repeat;
		background-size: cover;
		image-rendering: crisp-edges;
		filter: var(--cool-filter);
		z-index: -1;
	}
	.boxes {
		height: 100%;
		width: 100%;
		display: flex;
		flex-direction: column;
		gap: 25vw;

		margin-top: 85vw;
	}
	.box {
		font-size: 5vw;
		display: flex;
		flex-direction: column;
		background: black;
		border: 1px solid white;
		padding: 4vw;
		width: fit-content;
	}
	.about {
		align-self: self-end;
		width: fit-content;
		font-size: 8vw;
	}
	.showcase {
		font-size:5vw
	}
	.name {
		/* display: none; */
		font-size: 11vw;
		white-space: nowrap;
		transform: rotate(-50deg) translate(-18%, 100%);
		background: black;
	}
	
	h1,
	p {
		font-family: 'PP Mondwest Bold';
		font-size: inherit;
		color: white;
		image-rendering: pixelated;
		filter: var(--cool-filter);
	}

	:global(body) {
		background-color: black;
		background-size: cover;
		image-rendering: pixelated;
		image-rendering: crisp-edges;
		background-repeat: no-repeat;
		/* max-width: 100rem; */
		overflow-x: hidden;
		/* width: 100vw; */
		/* cool case where overflow-y actually effects */
		/* (its the name that overflowing on the btm)  */
		/* overflow-y: hidden; */
		/* tall screens ONLY */
		/* max-height: 100vh; */
	}

	/* write a media query that applys styles to desktop screens */
	@media (min-width: 1024px) {
		:global(body) {
			/* max-height: initial; */
			/* height: 200vh; */
			/* overflow-y: auto !important; */
		}
		section {
			/* height: 200vh; */
			/* max-height: 200vh; */
			/* position: relative; */
		}
		.boxes {
			/* margin-top: 100vh; */
		}
		.about {
			/* height: auto !important; */
			/* position: absolute; */
		}
	}
	/* media query for xl-wide screens that caps the width of the site */
	/* probably have to change vw units to something else  */

	/* make an alternate version of the site with a white background */
	/* trust me it looks suoer cool */
	@media (prefers-color-scheme: light) {
		:global(body) {
			background-color: white !important;
			filter: invert(1);
		}
		h1,
		p {
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
</style>
