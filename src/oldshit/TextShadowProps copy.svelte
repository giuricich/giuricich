<script lang="ts">
        type TextShadowData = {
                offsetX: number;
                offsetY: number;
                blurRadius: number;
                color: string;
                [key: string]: number | string;
        }
        export let data: TextShadowData;

    const handleInput = (e: Event) => {
        if (e.target instanceof HTMLInputElement) {
            const key = e.target.id;
            if (key) {
                data[key] = parseInt(e.target.value);
            }
        }
    }

    const handleColor = (e: Event) => {
        if (e.target instanceof HTMLInputElement) {
            data.color = e.target.value;
        }
    }


</script>
<section class="box">
    <h1>text-shadow</h1>
    <label for="offsetX">offset-x</label>
    <input type="range" name="offsetX" id="offsetX" min="-100" max="100" value={data.offsetX} on:input={handleInput}>
    <label for="offsetY">offset-y</label>
    <input type="range" name="offsetY" id="offsetY" min="-100" max="100" value={data.offsetY} on:input={handleInput}>
    <label for="blurRadius">blur-radius</label>
    <input type="range" name="blurRadius" id="blurRadius" min="-5" max="100" value={data.blurRadius} on:input={handleInput}>
    <label for="color">color</label>
    <input type="color" name="color" id="color" value={data.color} on:input={handleColor}>
</section>

<style>
    section {
        position: absolute;
        top: 0;
        right: 0;
        background-color: white;
        display: flex;
        flex-direction: column;
        align-items: center;
        padding: 2rem;
        width: 20rem;
        
    }
    h1 {
        margin-top: 0;
        font-size: 2rem;
    }
    label {
        margin-top: 0.5rem;
        font-size: 1.4rem;
    }
 
</style>

