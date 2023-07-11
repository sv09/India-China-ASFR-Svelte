<script>
    export let data;
    export let yScale;
    export let xScale;
    export let margin;
    export let height;
    export let year;

    let plotData = data.filter(d => d.Time === year);
</script>

<g transform="translate({margin.left}, {-margin.bottom})">
    {#each plotData as d}
        <rect x={xScale(d.AgeGrp)} y={yScale(d.ASFR)} width={xScale.bandwidth()-2} height={ height-yScale(d.ASFR)-margin.bottom } fill="rgb(119, 95, 160)"></rect>
    {/each}  
</g>

<style>

</style>