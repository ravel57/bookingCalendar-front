<template>
  <tr>
    <td>
      <div class="time-line" :style="{left: getDateNow}"/>
    </td>
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

  name: "timeLine",

  data() {
    return {
      hours: ['8:00', '9:00', '10:00', '11:00', '12:00', '13:00', '14:00', '15:00', '16:00', '17:00', '18:00', '19:00'],
      dataNow: new Date(),
      dateTimeLine: '',
    }
  },

  methods: {
    calcDateLine() {
      // console.log(this.dataNow)
      this.dateTimeLine = (((this.dataNow.getHours() - 7) * 60.35 + this.dataNow.getMinutes()) / 60 * 100) + '%'
      console.log(this.dateTimeLine)
      this.dataNow = new Date()
      setInterval(() => {
        // console.log(this.dataNow)
        console.log(this.dateTimeLine)
        this.dateTimeLine = (((this.dataNow.getHours() - 7) * 60.35 + this.dataNow.getMinutes()) / 60 * 100) + '%'
        this.dataNow = new Date()
      }, 60000)
    }
  },

  mounted: function () {
    this.calcDateLine()
  },

  computed: {
    getDateNow() {
      return this.dateTimeLine
    }
  }

}

</script>

<style>

.hour {
  margin: auto;
  min-width: 75px;
  text-align: center;
  padding: 5px 0;
}

.time-line {
  top: 100px;
  height: 30px;
  width: 1px;
  background: brown;
  position: relative;
  transform: scale(5.58);
}


</style>
