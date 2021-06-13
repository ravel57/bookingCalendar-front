<template>
  <tr>
    <td/>
    <td
        class="hour"
        v-for="(item, i) in hours"
        :key="i"
    >
      {{ item }}
    </td>
  </tr>
</template>

<script>
export default {
  name: "hours",

  data() {
    return {
      hours: ['8:00', '9:00', '10:00', '11:00', '12:00', '13:00', '14:00', '15:00', '16:00', '17:00', '18:00', '19:00']
    }
  },
}
</script>

<style>
.hour {
  margin: auto;
  min-width: 75px;
  text-align: center;
  padding: 5px 0;
}
</style>
