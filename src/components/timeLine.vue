<template>
  <tr>
    <td v-if="dataNow.getHours() > 8 & dataNow.getHours() < 18">
      <div class="time-line" :style="{left: getDateNow}"/>
    </td>
    <td v-else/>
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
      this.dateTimeLine = (((this.dataNow.getHours() - 7) * 60.7 + this.dataNow.getMinutes()) / 60 * 100) + '%'
      this.dataNow = new Date()
      setInterval(() => {
        this.dateTimeLine = (((this.dataNow.getHours() - 7) * 60.7 + this.dataNow.getMinutes()) / 60 * 100) + '%'
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
  text-align: left;
  padding: 5px 0;
  left: -15px;
  position: relative;
}

.time-line {
  top: 84px;
  height: 30px;
  width: 2px;
  background: brown;
  position: relative;
  transform: scaleY(6.6);
}

.time-line2 {
  top: 55px;
  transform: scaleY(4.7);
}

.time-line1 {
  top: 28px;
  transform: scaleY(2.9);
}
/*top = 28x - 0,3333*/
/*scaleY = 1,85x + 8,4333 */

</style>
