<script>    
    export let yVal;
    export let margin;
    export let yScale;

    let yTickVal = [];
    for(let i=Math.ceil(yVal[0])*10; i<Math.ceil(yVal[1]); i+=10){
        yTickVal.push(i);
    } 
</script>

<g>
    {#each yTickVal  as val}
        <text 
            x={margin.left} 
            y={yScale(val)}> {val} 
        </text>
    {/each}
</g>