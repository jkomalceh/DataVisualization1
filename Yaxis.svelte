<script>
    export let height;
    export let yScale;
    export let width;
    export let margin;
    console.log(height)
    let yTicks =[0,1,2,3,4,5,6];
</script>

<g transform="translate({margin.left} {margin.top})">
    {#each yTicks as tick }
        <text x={0} 
             y={yScale(tick)}
             dy="-5"
             dx="-10"
             >{tick} {tick== 6 ? 'Vendors': ''} </text>
        <line x1="0" 
            y1={yScale(tick)} 
            x2={width} 
            y2={yScale(tick)} 
            stroke="gray" />
     {/each}
</g>