<template>
<div id='main' style="width:500px; height:500px;" > 
 <!-- <e-chart id='main' :option="option"></e-chart> -->
</div>
 
</template>
<script setup lang="ts">
// import * as echarts from "echarts/core"
import { VueEcharts } from "vue3-echarts"
import {computed, onMounted, ref, defineProps} from 'vue'
import * as echarts from 'echarts';

type EChartsOption = echarts.EChartsOption;
const props = defineProps({
    options: Object
})
// onMounted(() => )
// import {PieChart} from 'echarts/charts'
// import { TitleComponent, TooltipComponent, 
//         GridComponent, DatasetComponent, TransformComponent} from 'echarts/components'
// import { LabelLayout, UniversalTransition} from 'echarts/features'
// import { CanvasRenderer } from 'echarts/renderers'
// echarts.use([])
// let chartDOM = ref(new HTMLElement())
// let chart = echarts.init(chartDOM)
// let options:EChartsOption;
onMounted(() => option())
// var option: EChartsOption;
let option = () => {
    // title: {
    //     name: 'Statistic'
    // },
    // tooltip:{},
    // legend:{},
let chart = echarts.init(document.getElementById('main'))
let option = {
  title: {
    text: 'Referer of a Website',
    subtext: 'Fake Data',
    left: 'center'
  },
  tooltip: {
    trigger: 'item'
  },
  legend: {
    orient: 'vertical',
    left: 'left'
  },
  series: [
    {
      name: 'Access From',
      type: 'pie',
      radius: '50%',
      data: props.options
    }
  ]
};
chart.setOption(option)
    }

   
</script>
<style scoped>
    #chart{
        height: 500px;
        width: 500px;
    }
    
</style>