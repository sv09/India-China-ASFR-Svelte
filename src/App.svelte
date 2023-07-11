<script>
	import fertilityData from "./data/India_China_data.js";
	import AxisX from "./components/AxisX.svelte";
	import AxisY from "./components/AxisY.svelte"; 
	import VerticalBar from "./components/VerticalBar.svelte";
	import { scaleBand, scaleLinear, extent } from "d3";
	// console.log(fertilityData);

	fertilityData.forEach(d => {
		d.ASFR = +d.ASFR;
	});

	let year = "2021";

	let data2021 = fertilityData.filter(d => d.Time === year);
	let IndiaData = fertilityData.filter(d => d.Location === "India");
	let ChinaData = fertilityData.filter(d => d.Location === "China");

	const margin = { top: 30, right: 30, bottom: 30, left: 40 };
	const width = 600 - margin.left - margin.right;
	const height = 400 - margin.top - margin.bottom;

	//India
	const xValL = [];
	IndiaData.map(d => d.Time === year ? xValL.push(d.AgeGrp) : '');
	const xScaleL = scaleBand()
					.domain(xValL)
					.range([margin.left, width-margin.right]);


	const yVal = extent(data2021, d => d.ASFR);
	const yScale = scaleLinear()
					.domain(yVal)
					.range([height-margin.bottom, margin.top]);

	//China
	const xValR = [];
	ChinaData.map(d => d.Time === year ? xValR.push(d.AgeGrp) : '');
	const xScaleR = scaleBand()
					.domain(xValR)
					.range([margin.left, width-margin.right]);


</script>

<main>
	<div class="wrapper">
		<h3>Age Specific Fertility Rate (ASFR) by age groups of 5 in India and China</h3>
		<svg class="contentL" {width} {height}>
			<AxisX xVal={xValL} {margin} {height} xScale={xScaleL}/>
			<AxisY {yVal} {margin} {yScale}/>
			<VerticalBar data={IndiaData} xScale={xScaleL} {yScale} {margin} {height} {year}/>
		</svg>
		<svg class="contentR" {width} {height}>
			<AxisX xVal={xValR} {margin} {height} xScale={xScaleR}/>
			<!-- <AxisY {yVal} {margin} {yScale}/> -->
			<VerticalBar data={ChinaData} xScale={xScaleR} yScale={yScale} {margin} {height} {year}/>
		</svg>
	</div>
	
</main>

<style>
	.wrapper{
		display: grid;
		grid-template-columns: repeat(10, 1fr);
		font-size: 12px;
	}
	h3{
		grid-column: 3 / 9;
		justify-self: center;
		font-size: 18px;
		margin-bottom: 50px;
	}
	.contentL{
		grid-column: 1 / 5;
		
	}
	.contentR{
		grid-column: 5 / 11;
	}
</style>