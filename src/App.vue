<template>
  <div id="app">
    <link rel="preconnect" href="https://fonts.gstatic.com">
    <link href="https://fonts.googleapis.com/css2?family=Ubuntu:wght@300&display=swap" rel="stylesheet">
<!--    <booked-list/>-->
    <calendar/>
  </div>
</template>

<script>
import calendar from './components/calendar.vue'
// import bookedList from "@/components/bookedList";

export default {
  name: 'App',
  components: {
    // bookedList,
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
  font-family: 'Ubuntu', sans-serif;
  display: flex;
}


</style>
