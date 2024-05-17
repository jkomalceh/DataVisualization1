<script>
export let data;
export let xScale;
export let yScale;

$: console.log(xScale(data.Percentage))
</script>

<div class='tooltip' style="position: absolute;
    top: {yScale (data.vendor)}px;
    left: {xScale (data.Percentage)}px">
<h1>Material: {data.material} </h1>
<p> Vendor: {data.vendor}</p>
</div>

<style>
    .tooltip{
        padding: 3px;
        background: rgba(235, 235, 212, 0.384);
        border: 1px solid rgba(0, 0, 0, 0.5);
        pointer-events: none;
        border-radius: 6px;
        opacity: 50;
        transition: top 300ms ease; left: 300ms ease;
    }
    h1{
        font-weight: 700;
        margin-bottom: 0.25rem;
    }
</style>