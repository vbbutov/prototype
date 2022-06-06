<template>
    <div>
        <h2>Статистика состояний объектов мониторинга</h2>
        <div>
            <ul>
                <li>Всего: {{get100Procent()}}</li>
                <li  v-for="e in metric()" :key="e">
                    <div :class="e.state"></div>
                    {{e.state}} {{ getProcent(e)* 100}}%
                </li>
            </ul>
        </div>
    </div>
</template>
<script setup lang="ts">
import {a} from '@/ListObject'
import { computed } from 'vue'
    const listJSON = JSON.stringify(a)
    // получил массив
    const allStatuses = new Set(JSON.parse(listJSON).map(data => (data.status)))
    const list = JSON.parse(listJSON).map(data => ({"status":data.status}))
    // const list1 = JSON.parse(listJSON).map(data => ({"status":data.status,  "count": 0 }))
    const metric = () => {
        let result = []
        allStatuses.forEach(state =>{
            let s = list.filter(e => e.status === state)
            // console.log("state "+ s.length)
            result.push({"state" : state, "count": s.length })
        })
        // console.log(result)
        return result
    }
    const get100Procent = () =>{ 
        let all = 0
        metric().forEach(e => {
           // console.log(e)
            all +=e.count
       //     console.log("this all ="+all)
        })
        return all
    }
    const getProcent = (e) => {
        console.log(e)
        return ((get100Procent()/100) * e.count).toFixed(1)
         }


    // const mapList1= computed(() => {
    //   let result:object[] = [] 
    //   list1.forEach(e => {
    //       console.log("Содержимое массива " + JSON.stringify(result))
    //     let find = ((e) => {
    //         if(result.length < 0 ){
    //             return false
    //         }
    //         for(let i in result) {
    //              console.log("e= " + e.status);
    //              if( i.status === e.status){
    //                  console.log(result[i])
    //                  return true
    //              }
    //         }
    //         return false
    //         })
    //     console.log("find "+ find(e))
    //     console.log("indexOF" + list1.indexOf("status"))
    //      console.log("=========================")
    
    //   }) 
    //   return result 
    // })
 
</script>
<style>
 li{
     list-style-type:none;
 }
 .ok{
     width: 15px;
     height: 15px;
     border: 2px solid green;
     border-radius: 50%;
     background-color:green;
 }
  .error{
    width: 15px;
     height: 15px;
     border: 2px solid red;
     border-radius: 50%;
     background-color: red;
 }
  .warning{
    width: 15px;
     height: 15px;
     border: 2px solid yellow;
     border-radius: 50%;
     background-color: yellow;
 }
 .critical{
      width: 15px;
     height: 15px;
     border: 2px solid brown;
     border-radius: 50%; 
     background-color: brown;
 }
 .circle{

 }
</style>