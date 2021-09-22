<script>
  import { getContext } from 'svelte';

  export let scale;
  export let label;

  const { dimensions: dimensionsStore } = getContext('chart');
  $: dimensions = $dimensionsStore;

  $: [xMin, xMax] = scale.range();
</script>

<g transform={`translate(0 ${dimensions.boundedHeight})`}>
  <text class="axis__label" x={(xMax - xMin) / 2} text-anchor="middle" y={40}>
    {label}
  </text>
</g>

<style>
  .axis__label {
    fill: #282828;
  }
</style>
