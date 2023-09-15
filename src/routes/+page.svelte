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

	let shadowThicknes = ".1vw";
	let dotThinkness = ".5vw";

	let styles = {
		shadow: '0 0 1px black',
		'many-shadows': '0 0 1px black,',
		'cool-filter': `drop-shadow(-${shadowThicknes} -${shadowThicknes} 0 red) drop-shadow(${shadowThicknes} ${shadowThicknes} 0 blue)`,
		'dot-filter': `drop-shadow(-${dotThinkness} -${dotThinkness} 0 red) drop-shadow(${dotThinkness} ${dotThinkness} 0 blue)`,
		'invert-filter': `drop-shadow(-${shadowThicknes} -${shadowThicknes} 0 cyan) drop-shadow(${shadowThicknes} ${shadowThicknes} 0 yellow)`
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
			<p>i do cool internet stuff</p>
			<p><em>i wish i were a bird</em></p>
		</div>
		<div class="box showcase">
			<h1 class="middle">check out!</h1>
			<p><a href="https://fallingpizza11.itch.io/cozy-city-builder">this</a> dumb game i made</p>
			<p>or <a href="https://devpost.com/software/tutr-ksez81">this</a> really silly hackathon project!</p>
			<p>and its much better looking <a href="https://github.com/giuricich/onliClass-darkmode">darkmode cousin</a>... if you can even build it lol</p>
			<p>cant forget the infinitely scalable <em>all the small things</em> single cover <a href="https://destructive.space">made intierly of css!</a></p>
		</div>
		<div class="box contact">
			<h1 class="middle">more isaac...</h1>
			<a href="https://github.com/giuricich">github</a>
			<a href="https://www.linkedin.com/in/isaac-giuricich/">linkedin</a>
		<a href="mailto:isaac@giuricich.ca">isaac@giuricich.ca</a>
		</div>
	</div>
</section>

<style>
	@import url('reset.css');
	@font-face {
		font-family: 'PP Mondwest Bold';
		src: url('/PPMondwest-Bold.woff') format('woff');
	}
	.middle {
		align-self: center;
	}


	section {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
		position: relative;
		/* for name text overflow */
		width: 100%;
		/* max-width: min(100vw, 100vh); */
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
		filter: var(--dot-filter);
		z-index: -1;
	}
	.boxes {
		height: 100%;
		width: 100%;
		display: flex;
		flex-direction: column;
		gap: 5vw;

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
		font-size:5vw;
	}
	.showcase h1 {
		font-size: 6vw;
	}
	.showcase p {
		line-height: normal;
		margin-top: 3vw;
		margin-bottom: 3vw;
	}
	.name {
		/* display: none; */
		font-size: 11vw;
		white-space: nowrap;
		transform: rotate(-50deg) translate(-18%, 100%);
		background: black;
	}
	
	h1,
	p,
	a {
		font-family: 'PP Mondwest Bold';
		font-size: inherit;
		color: white;
		image-rendering: pixelated;
		filter: var(--cool-filter);
	}
	a:hover {
		/* color: blue; */
		/* color: black; */
		filter: var(--dot-filter);
		transition: filter 400ms cubic-bezier(0.165, 0.84, 0.44, 1);
	}

	:global(body) {
		background-color: black;
		background-size: cover;
		image-rendering: pixelated;
		image-rendering: crisp-edges;
		background-repeat: no-repeat;
		/* max-width: 100rem; */
		overflow-x: hidden;
		display: flex;
		flex-direction: column;
		align-items: center;
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
