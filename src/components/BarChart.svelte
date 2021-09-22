<script>
  import * as d3 from 'd3';
  import Chart from './Chart/Chart.svelte';
  import XAxis from './Chart/XAxis.svelte';
  import YAxis from './Chart/YAxis.svelte';
  import Tooltip from './Chart/Tooltip.svelte';

  export let data;

  const xAccessor = d => d.year;
  const yAccessor = d => +d.percentage;

  let width = 100;
  let height = 100;

  let hoveredBar = null;

  const margins = {
    marginTop: 40,
    marginRight: 20,
    marginBottom: 65,
    marginLeft: 45,
  };

  $: dms = {
    width,
    height,
    ...margins,
    boundedHeight: Math.max(
      height - margins.marginTop - margins.marginBottom,
      0,
    ),
    boundedWidth: Math.max(width - margins.marginLeft - margins.marginRight, 0),
  };

  $: xScale = d3
    .scaleBand()
    .domain(data.map(d => d.year))
    .rangeRound([0, dms.boundedWidth])
    .padding(0.05);

  $: yScale = d3
    .scaleLinear()
    .domain([0, d3.max(data, yAccessor)])
    .range([dms.boundedHeight, 0])
    .nice();

  const handleMouseEnter = d => {
    hoveredBar = d;
  };

  const handleMouseLeave = () => {
    hoveredBar = null;
  };
</script>

<div
  class="bar-chart__placeholder"
  bind:clientWidth={width}
  bind:clientHeight={height}
>
  <Chart dimensions={dms}>
    {#each data as d}
      <rect
        x={xScale(xAccessor(d))}
        y={yScale(yAccessor(d))}
        width={xScale.bandwidth()}
        height={dms.boundedHeight - yScale(yAccessor(d))}
        on:mouseenter={handleMouseEnter(d)}
        on:mouseleave={handleMouseLeave}
      />
    {/each}
    <XAxis scale={xScale} label="year" />
    <YAxis scale={yScale} label="foreign-born population (%)" />
    {#if hoveredBar}
      <Tooltip
        {hoveredBar}
        {xScale}
        {yScale}
        boundedHeight={dms.boundedHeight}
      />
    {/if}
  </Chart>
</div>

<style>
  .bar-chart__placeholder {
    position: relative;
    font-size: 16px;
    width: 100%;
    height: 300px;
    max-width: 700px;
    margin: 0 40px;
  }

  rect {
    fill: #4427ca;
  }

  rect:hover {
    fill: #dc267f;
  }
</style>
