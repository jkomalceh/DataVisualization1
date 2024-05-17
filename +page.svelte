<script>
    import data from "./data.js";
    console.log(data);

    let width=400;
    let height=400;

    const margin = { top:20, right:15, left:10, bottom:20};

    import { scaleLinear } from "d3-scale";
    $: xScale = scaleLinear()
        .domain([0, 100]) 
        .range([0, width - margin.left- margin.right]);

    import {max} from "d3-array";
        const yScale = scaleLinear()
        .domain([0, max(data, d => d.vendor)])
        .range([height - margin.top - margin.bottom, 0]);

    import AxisX from "./Xaxis.svelte";
    import AxisY from "./Yaxis.svelte";
    import Tooltip from "./Tooltip.svelte";

    let hoveredData;
    $: console.log(hoveredData);
</script>

<h1>Percentage of material availabel per vendors</h1>
<div class="chart-container" 
    bind:clientWidth={width}
    on:mouseleave={() => {
        hoveredData = null;
    }} >
<svg {width} {height}>
<AxisX {height} {xScale} {margin}/>
<AxisY {height} {width} {yScale} {margin} />
<g class='circles' transform="translate({margin.left} {margin.top})">
   {#each data.sort((a,b) => a.Percentage - b.Percentage) as vend}
    {#if vend.material ==1}
        <circle cx={xScale (vend.Percentage)} cy={yScale(vend.vendor)} 
        r={hoveredData && hoveredData == vend ? "30" : "19" }
        opacity={hoveredData && hoveredData == vend ? "1" : ".3" }
        fill="green" stroke="black"
        on:mouseover={() => {
            hoveredData = vend;
             }}
        on:focus={() => {
            hoveredData = vend;
        }}
        tabindex=0;
        />
    {:else if vend.material == 2}
        <circle cx={xScale (vend.Percentage)} cy={yScale(vend.vendor)} 
        r={hoveredData && hoveredData == vend ? "30" : "13" }
        opacity={hoveredData && hoveredData == vend ? "1" : ".3" }
        fill="purple" stroke="blcak"
        on:mouseover={() => {
            hoveredData = vend;
             }}
        on:focus={() => {
            hoveredData = vend;
        }}
        tabindex=0;
        />
    {:else}
        <circle cx={xScale (vend.Percentage)} cy={yScale(vend.vendor)} 
        r={hoveredData && hoveredData == vend ? "30" : "7" }
        opacity={hoveredData && hoveredData == vend ? "1" : ".3" }
        fill="red" stroke="black" 
        on:mouseover={() => {
            hoveredData = vend;
             }}
        on:focus={() => {
            hoveredData = vend;
        }}
        tabindex=0;
        />
    {/if} 
   {/each}
</g>
</svg>
{#if hoveredData}
	<Tooltip data={hoveredData} {xScale} {yScale}/>
{/if}
</div>

<style>
    circle{
        transition: all 300ms ease;
        cursor: pointer;

    }

    circle:focus{
        outline: none;
    }
    h1{
        font-size: 1.5rem;
        font-weight: 600;
       
        width:500px;
    margin: 0 auto;
    background: rgba(10, 203, 65, 0.422);
    text-align: center;
        
    }
</style>