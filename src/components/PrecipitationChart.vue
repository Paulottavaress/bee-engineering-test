<template>
  <div v-if="!loading">
    <Bar
      :chart-options="chartOptions"
      :chart-data="chartData"
      :chart-id="chartId"
      :dataset-id-key="datasetIdKey"
      :plugins="plugins"
      :css-classes="cssClasses"
      :styles="styles"
      :width="width"
      :height="height"
    />
  </div>
  <div v-else class="container-gif">
    <img src="/public/images/loading-buffering.gif" alt="">
  </div>
</template>

<script>
 import { Bar } from 'vue-chartjs';
 import { Chart as ChartJS, Title, Tooltip, Legend, BarElement, CategoryScale, LinearScale } from 'chart.js';
 import axios from 'axios';

ChartJS.register(Title, Tooltip, Legend, BarElement, CategoryScale, LinearScale)

export default {
  name: 'PrecipitationChart',
  components: { Bar },
  props: {
    chartId: {
      type: String,
      default: 'bar-chart'
    },
    datasetIdKey: {
      type: String,
      default: 'label'
    },
    width: {
      type: Number,
      default: 400
    },
    height: {
      type: Number,
      default: 400
    },
    cssClasses: {
      default: '',
      type: String
    },
    styles: {
      type: Object,
      default: () => {}
    },
    plugins: {
      type: Object,
      default: () => {}
    },
    chartInfo: {
      type: Object,
      default: () => {}
    }
  },
  data() {
    return {
      chartData: {
        labels: [],
        datasets: [ { data: [] } ]
      },
      chartOptions: {
        responsive: true
      },
      loading: true
    }
  },
  mounted() {
    navigator.geolocation.getCurrentPosition(this.showPosition);
  },
  methods: {
    showPosition(position) {
      this.loading = true;

      axios.get(`https://api.open-meteo.com/v1/forecast?latitude=${position.coords.latitude}&longitude=${position.coords.longitude}&daily=precipitation_sum&timezone=UTC&past_days=2`)
      .then((response) => {
        const precipitation = response.data.daily.precipitation_sum;
        const day = response.data.daily.time;
        this.chartData.labels = day;
        this.chartData.datasets[0].data = precipitation;
      })
      .catch(function (error) {
        console.log(error);
      })
      .then(() => {
        this.loading = false;
      })
    }
  }
}
</script>

<style lang="scss" scoped>
  .container-gif {
    max-width: 50px;
    max-height: 50px;

    img {
      max-width: 100%;
      height: 100%;
    }
  }
</style>