<script lang="ts">
	import { text } from '@sveltejs/kit';
  import TextShadowProps from './TextShadowProps.svelte';


    let textShadowData = {
        offsetX: 0,
        offsetY: 0,
        blurRadius: 0,
        color: '#fff',
    };

    $: textShadow = `
        ${textShadowData.offsetX}px
        ${textShadowData.offsetY}px
        ${textShadowData.blurRadius}px
        ${textShadowData.color}
    `;
    $: paragraphStyle = `
        text-shadow: ${textShadow};`


</script>

<section>
    <h1 style={paragraphStyle}>hello</h1>
    <p>its a me</p>
    <p>{textShadow}</p>
    <TextShadowProps bind:data={textShadowData}></TextShadowProps>
</section>

<style>
    :global(body) {
        background: url("/images/dots.png");
        background-size: cover;
        image-rendering: pixelated;
        image-rendering: crisp-edges;
        background-repeat: no-repeat;
    }
    section {
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
    }
    h1, p {
        font-family: 'Press Start 2P', cursive;
        font-size: 3rem;
        color: #fff;
        text-shadow: 0 0 5px #fff;
        background-color: black;
        border-radius: 12px;
    }
</style>