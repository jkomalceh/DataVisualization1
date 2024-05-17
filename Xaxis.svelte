<script>
    export let height;
    export let xScale;
    export let margin;
    console.log(height)
    let xTicks =[0,25,50,75,100];
</script>

<g>
    {#each xTicks as tick }
        <text x={xScale(tick)} 
        y={height - margin.bottom}
        dy="6"
        dx="10"
        dominant-baseline="hanging"
        text-anchor="middle"
        >{tick}%</text>
     {/each}
</g>