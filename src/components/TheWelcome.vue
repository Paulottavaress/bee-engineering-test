<template>
  <div class="container">
    <main>
      <h1>Welcome to DataHow - weatherAPI</h1>
      <h3>Progression and moving average of the historical and predicted precipitation at your location</h3>
      <div class="chart-container">
        <PrecipitationChart />
      </div>
      <h3>Progression and moving average of the historical and predicted temperature at your location</h3>
      <div class="chart-container">
        <TemperatureChart />
      </div>
    </main>
  </div>
</template>

<script>
import PrecipitationChart from './PrecipitationChart.vue';
import TemperatureChart from './TemperatureChart.vue';

export default {
  components: { 
    PrecipitationChart, 
    TemperatureChart 
  },
}
</script>

<style lang="scss" scoped>
  .container {
    max-width: 1440px;
    padding: 2rem;
    margin: auto;

    main {
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      gap: 20px;

      h1, h3 {
        margin: 0px;
      }

      h1 {
        margin-bottom: 0.7rem;
        color: #FF2600;
      }
    }
  }
</style>

<style>
  #bar-chart {
    max-width: 100%;
  }
</style>

