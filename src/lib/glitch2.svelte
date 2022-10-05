<script lang="ts">
    import Glitch1 from "./glitch1.svelte";
    export let text = "Glitch";
    let i:number;
    $: letters = text.split("");
    $: getRandom = ()=> i + Math.random();
    setInterval(() =>  {
        i = Math.random() * .002;
        // const _text = text;
        // text = text.toLowerCase();
        // setTimeout(() => {
        //     text = _text;
        // }, 40);
    }, 500);
</script>


{#each letters as letter}
    <Glitch1 text={letter} delayMs={getRandom()*500} amountTopPct={getRandom()*50} amountBtmPct={getRandom()*50}/>
{/each}

