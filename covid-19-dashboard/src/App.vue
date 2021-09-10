<template>
  <div class="container">
    <div class="row mt-5">
      <div class="col">
        <h1 class="text-center">COVID-19 DATA</h1>
      </div>
    </div>
    <div class="row mt-5" v-if="arrPositive.length > 0">
      <div class="col">
        <h2 class="text-center">Confirmed Cases</h2>
        <line-chart
          :chartData="arrConfirmed"
          :options="chartOptions"
          :chartColors="positiveChartColors"
          label="Positive"
        />
      </div>
    </div>

    <div class="row mt-5" v-if="arrHospitalized.length > 0">
      <div class="col">
        <h2 class="text-center">Cases on Admission</h2>
        <line-chart
          :chartData="arrAdmitted"
          :options="chartOptions"
          :chartColors="hospitalizedChartColors"
          label="Hospitalized"
        />
      </div>
    </div>

    <div class="row mt-5" v-if="arrRecovered.length > 0">
      <div class="col">
        <h2 class="text-center">Discharged</h2>
        <line-chart
          :chartData="arrDischarged"
          :options="chartOptions"
          :chartColors="recoveredColors"
          label="Recovered"
        />
      </div>
    </div>

    <div class="row mt-5 mb-5">
      <div class="col">
        <h2 class="text-center">Deaths</h2>
        <line-chart
          v-if="arrDeaths.length > 0"
          :chartData="arrDeaths"
          :options="chartOptions"
          :chartColors="deathColors"
          label="Deaths"
        />
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
// import moment from 'moment'
import LineChart from './components/LineChart'
export default {
  components: {
    LineChart,
  },
  data() {
    return {
      arrConfirmed: [],
      positiveChartColors: {
        borderColor: '#077187',
        pointBorderColor: '#0E1428',
        pointBackgroundColor: '#AFD6AC',
        backgroundColor: '#74A57F',
      },
      arrAdmitted: [],
      hospitalizedChartColors: {
        borderColor: '#251F47',
        pointBorderColor: '#260F26',
        pointBackgroundColor: '#858EAB',
        backgroundColor: '#858EAB',
      },
      // arrInIcu: [],
      // inIcuColors: {
      //   borderColor: '#190B28',
      //   pointBorderColor: '#190B28',
      //   pointBackgroundColor: '#E55381',
      //   backgroundColor: '#E55381',
      // },
      // arrOnVentilators: [],
      // onVentilatorsColors: {
      //   borderColor: '#784F41',
      //   pointBorderColor: '#784F41',
      //   pointBackgroundColor: '#BBE5ED',
      //   backgroundColor: '#BBE5ED',
      // },
      arrDischarged: [],
      recoveredColors: {
        borderColor: '#4E5E66',
        pointBorderColor: '#4E5E66',
        pointBackgroundColor: '#31E981',
        backgroundColor: '#31E981',
      },
      arrDeaths: [],
      deathColors: {
        borderColor: '#E06D06',
        pointBorderColor: '#E06D06',
        pointBackgroundColor: '#402A2C',
        backgroundColor: '#402A2C',
      },
      chartOptions: {
        responsive: true,
        maintainAspectRatio: false,
      },
    }
  },
  async created() {
    const { data } = await axios.get('https://covidnigeria.herokuapp.com/api')

    data.forEach((d) => {
      // const date = moment(d.date, 'YYYYMMDD').format('MM/DD')

      const { confirm, admitted, discharged, death } = d
      this.arrConfirmed.push({ total: confirm })
      this.arrAdmitted.push({
        total: admitted,
      })
      this.arrDischarged.push({ total: discharged })
      this.arrDeaths.push({ total: death })
    })
  },
}
</script>

<style></style>
