<script>
  export let hoveredBar;
  export let xScale;
  export let yScale;
  export let boundedHeight;
</script>

<g>
  <text
    class="tooltip"
    x={xScale(hoveredBar.year) + xScale.bandwidth() / 2}
    y={boundedHeight + 20}
    text-anchor="middle"
  >
    {hoveredBar.year}
  </text>

  <text
    class="tooltip"
    x={xScale(hoveredBar.year) + xScale.bandwidth() / 2}
    y={xScale.bandwidth() < 30 ? 5 : yScale(hoveredBar.percentage) - 10}
    text-anchor="middle"
  >
    {hoveredBar.percentage}
  </text>
</g>

<style>
  .tooltip {
    fill: #282828;
  }
</style>
