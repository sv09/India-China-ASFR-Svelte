<script>
    export let margin;
    export let height;
    export let xVal;
    export let xScale;
</script>

<g transform="translate({margin.left}, 0)">
    {#each xVal as val}
        <text 
            x={xScale(val)} 
            y={height-margin.bottom}> {val}
        </text>
    {/each}
</g>