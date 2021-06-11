<template>
  <div id="app">
    <calendar/>
  </div>
</template>

<script>
import calendar from './components/calendar.vue'

export default {
  name: 'App',
  components: {
    calendar
  }
}
</script>

<style>


#app {
  height: 100%;
  width: 100%;
  margin: 0;
  padding: 0;
}
</style>
