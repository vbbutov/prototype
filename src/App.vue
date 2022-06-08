<template>
  <div>
    <my-metric></my-metric>
    <!-- <my-test></my-test> -->
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import MyMetric from '@/components/MyMetric.vue'


export default defineComponent({
  name: 'App',
  components: {MyMetric}
});
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
