<template>
  <div id="app">
    <MultiplyTable/>
  </div>
</template>

<script>
import MultiplyTable from './components/MultiplyTable.vue'

export default {
  name: 'App',
  components: {
    MultiplyTable
  }
}
</script>

<style>
  *{
    margin: 0;
    padding: 0;
  }
</style>
