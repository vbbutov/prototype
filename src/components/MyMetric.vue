<template>
<div></div>
    <div class="main">
        <h2>Статистика состояний объектов мониторинга</h2>
        <div class="percents"> 
            <ul>
                <li>Всего: {{list.length}}</li>
                 <div class="row">
                    <li  v-for="e in metric()" :key="e">
                        <span :class="e.name"></span>
                        {{e.name}} {{e.value }}
                    </li>
                </div>
            </ul>
        </div>
        <div class="chart">
            <my-chart :options="metric()"></my-chart>
                    <!-- <my-test :metric="procents()"></my-test> -->
            </div>
    </div>
</template>
<script setup lang="ts">
import {a} from '@/ListObject'
import { computed } from 'vue'
import MyChart from '@/components/MyChart.vue'

    const listJSON = JSON.stringify(a)
    const allStatuses = new Set(JSON.parse(listJSON).map(data => (data.status)))
    // здесь хранится массив статусов для дальнешего подсчета записей  
    const list = JSON.parse(listJSON).map(data => ({"status":data.status}))
    // получаем метрику 
    const metric = () => {
        let result = []
        allStatuses.forEach(state =>{
            let s = list.filter(e => e.status === state)
            // console.log("S=" +JSON.stringify(s))
           
            result.push({"name" : state, "value": s.length, "itemStyle": {"color": getColor(state)} })
        })
        return result
    }
    const get100Procent = () =>{ 
        let all = 0
        metric().forEach(e => {
            all +=e.count
        })
        return all
    }
    // const getProcent = (e) => ((get100Procent()/100) * e.count).toFixed(1)
    // получаем массив с содержащий цвета и процент 
    // const procents = () => {
    //     let procent = []
    //     metric().forEach((e) =>{
    //         let data = {}
    //             data.status = e.state,
    //             data.color = getColor(e.state)
    //             data.procent = ((e.count/get100Procent()) * 100).toFixed(1) 
    //         procent.push(data)
    //     })
    //     return procent
    // }
  const getColor =(e) => {
 
      let x = "black"
      switch(e){
          case "critical" : x=  "brown"; break
          case "ok" : x = "green"; break
          case "error" : x=  "red"; break
          case "warning" : x=  "yellow"; break
      }
      
      return x
  } 

 
</script>
<style>
 li{
     list-style-type:none;
 }
 .ok{
     display: inline-block;
     width: 15px;
     height: 15px;
     border: 2px solid green;
     border-radius: 50%;
     background-color:green;
 }
  .error{
       display: inline-block;
    width: 15px;
     height: 15px;
     border: 2px solid red;
     border-radius: 50%;
     background-color: red;
 }
  .warning{
       display: inline-block;
    width: 15px;
     height: 15px;
     border: 2px solid yellow;
     border-radius: 50%;
     background-color: yellow;
 }
 .critical{
      display: inline-block;
      width: 15px;
     height: 15px;
     border: 2px solid brown;
     border-radius: 50%; 
     background-color: brown;
 }
 .row{
      display: inline-block;
     display: inline-block;
     text-align: left;
     width: 50%;
 }
 .percents{
     display: inline-block;
     vertical-align: top;
     width: 50%;
 }
 .chart{
      display: inline-block;
       width: 50%;
 }

</style>