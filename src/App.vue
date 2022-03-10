<!-- unpkg -->
<script src="https://unpkg.com/@egjs/flicking/dist/flicking.pkgd.min.js" crossorigin="anonymous"></script>
<!-- cdnjs -->
<script src="https://cdnjs.cloudflare.com/ajax/libs/egjs-flicking/4.x.x/flicking.pkgd.min.js" crossorigin="anonymous"></script>

<template>
  <div id="app" class="container">
    <h2 class="center mt-5" style="background-color: orange;">COVID-19 Pandemic in the Philippines</h2>

    <Flicking :options="{ align: 'prev', circular: true }" @move-end="onMoveEnd">
      <div class="panel"><img src="./assets/covidvid.png" class="mt-5"></div>
      <div class="panel"><img src="./assets/covid6.png" class="mt-5"></div>
      <div class="panel"><img src="./assets/covid5.png" class="mt-5"></div>
      <div class="panel"><img src="./assets/covidvid.png" class="mt-5"></div>
    </Flicking>
      <br>
        <div class="mt-2" style="height: 120px; color: dark gray; text-align: left; font-size: 16px;">An acute respiratory illness in humans caused by a coronavirus, capable of producing severe symptoms and in some cases death, especially in older people and those with underlying health conditions. It was originally identified in China in 2019 and became pandemic in 2020. Due to the growing threat of the said coronavirus and also the continuous span of misleading information and speculations, we made the initiative to create a data visualization web application that will summarize the daily updated overall cases of COVID-19 in the Philippines to encompass a better understanding and awareness about the current situation being faced.</div>
      <br>
    <hr>

    <div class="row mt-5" v-if="arrInfected.length > 0">
      <div class="col">
        <h2>Positive Cases</h2>
         <div class="mt-2" style="height: 120px; color: dark gray; text-align: left; font-size: 16px;">Positive cases identify to be consisting in or characterized by the presence or possession of features or qualities of a COVID-19 infected person. The main line chart shows daily reported COVID-19 positive patients from April 2020 up to the present month, June 2021. It is classified with a line chart color of red and mapped out with date intervals of each month on the x axis of the graph, and the total of cases rounded off by tens on the y axis.</div>
        <line-chart :chartData="arrInfected" :options="chartOptions" label="Positive" :chartColors="infectedChartColors"></line-chart>
      </div>
    </div> 

      <button style="background-color: #83a95c; border-color: #70af85; color: white; display: inline; margin-top: 50px; margin-right: 40px; margin-left: 350px;" @click="showRecoveredChart = !showRecoveredChart">Compare with Recovered</button>
      <button style="background-color: #aa2ee6; border-color: #6155a6; color: white; display: inline; margin-top: 50px; margin-left: 30px;" @click="showDeceasedChart = !showDeceasedChart">Compare with Deceased</button>  
    <br>

    <div class="row mt-5" v-if="arrInfected.length > 0 && showRecoveredChart">
      <h2>Comparison between Positive and Recovered Cases</h2>
        <div class="col">
          <h2 class="mt-3">Positive</h2>
          <line-chart :chartData="arrInfected" :options="chartOptions" label="Positive" :chartColors="infectedChartColors"></line-chart>
        </div>
        <div class="col">
          <h2 class="mt-3">Recovered</h2>
          <line-chart :chartData="arrRecovered" :options="chartOptions" label="Recovered" :chartColors="recoveredChartColors"></line-chart>
        </div>
    </div> 


    <div class="row mt-5" v-if="arrInfected.length > 0 && showDeceasedChart">
      <h2>Comparison between Positive and Deceased Cases</h2>
        <div class="col">
          <h2 class="mt-3">Positive</h2>
          <line-chart :chartData="arrInfected" :options="chartOptions" label="Positive" :chartColors="infectedChartColors"></line-chart>
        </div>
        <div class="col">
          <h2 class="mt-3">Deceased</h2>
          <line-chart :chartData="arrDeceased" :options="chartOptions" label="Deceased" :chartColors="deceasedChartColors"></line-chart>
        </div>
    </div> 

  <hr>
    <div class="row mt-5" v-if="arrRecovered.length > 0">
      <div class="col">
        <h2>Recovered Cases</h2>
          <div class="mt-2" style="height: 120px; color: dark gray; text-align: left; font-size: 16px;">Recovered cases were once COVID-19 positive patients who have returned to a normal state of health, mind, and strength. They are no longer capable of spreading the coronavirus to others. The second line chart shows daily reported COVID-19 recovered patients from April 2020 up to the present month, June 2021. It is classified with a line chart color of green and mapped out with date intervals of each month on the x axis of the graph, and the total of cases rounded off by tens on the y axis.</div>
          <line-chart :chartData="arrRecovered" :options="chartOptions" label="Recovered" :chartColors="recoveredChartColors"></line-chart>
      </div>
    </div>

    <div class="row mt-5" v-if="arrDeceased.length > 0">
      <div class="col">
        <h2>Deceased Cases</h2>
          <div class="mt-2" style="height: 120px; color: dark gray; text-align: left; font-size: 16px;">Deceased cases were once COVID-19 positive patients who ceased living, succumbed to the coronavirus and died. Some deceased cases are counted days or weeks after a patient's death. The last line chart shows daily reported COVID-19 deceased patients from April 2020 up to the present month, June 2021. It is classified with a line chart color of violet and mapped out with date intervals of each month on the x axis of the graph, and the total of cases rounded off by tens on the y axis.</div>
          <line-chart :chartData="arrDeceased" :options="chartOptions" label="Deceased" :chartColors="deceasedChartColors"></line-chart>
        </div>
    </div> 


    <div class="row mt-5" v-if="arrRecovered.length > 0">
      <h2>Comparison between Recovered and Deceased Cases</h2>
        <div class="col">
          <h2 class="mt-3">Recovered</h2>
          <line-chart :chartData="arrRecovered" :options="chartOptions" label="Recovered" :chartColors="recoveredChartColors"></line-chart>
        </div>
        <div class="col">
          <h2 class="mt-3">Deceased</h2>
          <line-chart :chartData="arrDeceased" :options="chartOptions" label="Deceased" :chartColors="deceasedChartColors"></line-chart>
        </div>
    </div> 
    <br>

  <div class="row mt-5">
    <h2>Active Cases</h2>
    <div class="mt-2" style="height: 120px; color: dark gray; text-align: left; font-size: 16px;">Total active COVID-19 cases per month on the first half of 2021. The data is interpreted through a bar chart ascending from below, depicting higher numbers upon bars.</div>
    <bar-chart :chartData="arrActiveCases" :options="chartOptions" label="Active Cases" :chartColors="activeChartColors"></bar-chart>
  </div>
    <br>

    <hr>
    <div class="row mt-5">
    <h2>Summary of Cases</h2>
    <pie-chart></pie-chart>
  </div>

  </div>
</template>

<script>
import axios from 'axios';
import moment from 'moment';
import LineChart from './components/LineChart.vue';
import BarChart from './components/BarChart.vue';
import PieChart from './components/PieChart.vue';
export default {
  name: 'App',
  components: {
    LineChart,
    BarChart,
    PieChart
  },
  data() {
    return {
      arrInfected: [],
      infectedChartColors: {
        borderColor: "#cc561e",
        pointBorderColor: "#bd2000",
        pointBackgroundColor: "#f9f3f3",
        backgroundColor: "#e45826"
      },
      arrRecovered: [],
      recoveredChartColors: {
        borderColor: "#5aa469",
        pointBorderColor: "#adce74",
        pointBackgroundColor: "#f9f3f3",
        backgroundColor: "#61b15a"
      },
      arrDeceased: [],
      deceasedChartColors: {
        borderColor: "#413c69",
        pointBorderColor: "#709fb0",
        pointBackgroundColor: "#f9f3f3",
        backgroundColor: "#4a47a3"
      },
      arrActiveCases: [],
      activeChartColors: {
        backgroundColor: "#f87979"
      },
      date: [],
      chartOptions: {
        responsive: true,
        maintainAspectRatio: false
      },
      showRecoveredChart: false,
      showDeceasedChart: false
    }
  },
  async created() {
    const { data } = await axios.get("https://api.apify.com/v2/datasets/sFSef5gfYg3soj8mb/items?format=json&clean=1");
    data.forEach(d => {
      const lastUpdatedAtApify = moment(d.lastUpdatedAtApify, "YYYY-MM-DD'T'HH:mm:ss.SSS'Z'").format("MM/DD");
      const {
        infected,
        recovered,
        deceased,
        activeCases
      } = d;

      this.date.push({lastUpdatedAtApify});
      this.arrInfected.push({lastUpdatedAtApify, infected});
      this.arrRecovered.push({lastUpdatedAtApify, recovered});
      this.arrDeceased.push({lastUpdatedAtApify, deceased});
      this.arrActiveCases.push({lastUpdatedAtApify, activeCases});

      console.log(this.arrInfected);

    })
  },
};
</script>

<style>

  
</style>
