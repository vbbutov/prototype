<template>
  <div style="min-width: 200px">
    <DoughnutChart :chartData="metric"  :width='400' :height='400' :cssClasses='size'/>
  </div>
</template>

<script setup lang="ts">

import { ChartData } from 'chart.js';
import { computed, defineProps } from 'vue';
import { DoughnutChart } from 'vue-chart-3';
import {Chart, registerables} from "chart.js"
Chart.register(...registerables)
const props = defineProps({
    metric: Array,
    color: String
})
// const x = () => props.metric?.map
const procents = () => props.metric?.map( data => data.procent )
const color = () => props.metric?.map(data => data.color)
const states = () => props.metric?.map(data => data.status)
const metric:ChartData = {
    // передаем пока что статус
    labels: states(),
    datasets: [
        {
            // передаем проценты
            data: procents(),
            // передаем статаус
            backgroundColor: color()
        } 
    ]
}

</script>
<style scoped>
  .size{
    min-width: 1000px;
    min-height: 1000px;

  }
</style>