<script>
  import * as d3 from 'd3';
  import Header from './components/Header.svelte';
  import BarChart from './components/BarChart.svelte';
  import Footer from './components/Footer.svelte';

  let barChartData;

  d3.csv('../data/foreignBornPopulation.csv').then(
    data => (barChartData = data),
  );
</script>

<main>
  <div class="app">
    <Header />
    {#if barChartData}
      <BarChart data={barChartData} />
    {/if}
    <Footer />
  </div>
</main>

<style>
  @font-face {
    font-family: 'Merriweather';
    font-style: normal;
    font-weight: 700;
    src: local(''),
      url('../fonts/merriweather-v25-latin-700.woff2') format('woff2'),
      url('../fonts/merriweather-v25-latin-700.woff') format('woff');
  }

  @font-face {
    font-family: 'Source Sans Pro';
    font-style: normal;
    font-weight: 400;
    src: local(''),
      url('../fonts/source-sans-pro-v14-latin-regular.woff2') format('woff2'),
      url('../fonts/source-sans-pro-v14-latin-regular.woff') format('woff');
  }

  :root {
    font-family: 'Source Sans Pro', sans-serif;
    font-size: 16px;
    color: #282828;
    background: #ffffff;
    margin: 0 15px;
  }

  .app {
    display: flex;
    flex-direction: column;
    align-items: center;
    height: 100%;
    width: 100%;
    user-select: none;
  }
</style>
