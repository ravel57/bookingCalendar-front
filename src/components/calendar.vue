<template>
  <div id="calendar">
    <!--    <div class="tab">-->
    <!--      <h3>{{ thisDay(bron[0].date) }}</h3>-->
    <!--      <table style="width: inherit;">-->
    <!--        <time-line/>-->
    <!--        <tr v-for="(t, i) in bron[0].cabinets" :key="i">-->
    <!--          <td class="cabinet">{{ cabinets[t.cabinetId] }}</td>-->
    <!--          <td-->
    <!--              v-for="(g, j) in t.reserved"-->
    <!--              :key="j"-->
    <!--          >-->
    <!--            <div v-if="getLength(g)">-->
    <!--              <div-->
    <!--                  class="rectangle"-->
    <!--                  :style="{width: getLength(g), left: getLeft(g), background: g.color}"-->
    <!--              ><p>{{ g.name }}</p></div>-->
    <!--            </div>-->
    <!--          </td>-->
    <!--        </tr>-->
    <!--      </table>-->
    <!--    </div>-->
    <!--    <div-->
    <!--        class="tab"-->
    <!--        v-for="(ttt, ti) in bron.slice().slice(1)"-->
    <!--        :key="ti"-->
    <!--    >-->
    <!--      <h3>{{ thisDay(ttt.date) }}</h3>-->
    <!--      <table style="width: inherit;">-->
    <!--        <hours/>-->
    <!--        <tr-->
    <!--            v-for="(t, i) in ttt.cabinets"-->
    <!--            :key="i"-->
    <!--        >-->
    <!--          <td class="cabinet">{{ cabinets[t.cabinetId] }}</td>-->
    <!--          <td-->
    <!--              v-for="(g, j) in t.reserved"-->
    <!--              :key="j"-->
    <!--          >-->
    <!--            <div v-if="getLength(g)">-->
    <!--              <div-->
    <!--                  class="rectangle"-->
    <!--                  :style="{width: getLength(g), left: getLeft(g), background: g.color}"-->
    <!--              ><p>{{ g.name }}</p></div>-->
    <!--            </div>-->
    <!--          </td>-->
    <!--        </tr>-->
    <!--      </table>-->
    <!--    </div>-->
  </div>
</template>

<script>
const groupBy = key => array =>
    array.reduce((objectsByKeyValue, obj) => {
      const value = obj[key];
      objectsByKeyValue[value] = (objectsByKeyValue[value] || []).concat(obj);
      return objectsByKeyValue;
    }, {});
// import axios from "axios";
// import timeLine from "./timeLine";
// import hours from "./hours";

export default {
  name: 'calendar',

  components: {
    // timeLine,
    // hours,
  },

  data() {
    return {
      bron: [{
        "id": 1,
        "userId": 1,
        "cabinetId": 1,
        "startTime": 1635355114000,
        "duration": 50,
        "title": "---",
        "color": "240 147 23"
      }, {
        "id": 2,
        "userId": 1,
        "cabinetId": 1,
        "startTime": 1635519719000,
        "duration": 60,
        "title": "+++",
        "color": "150 16 90"
      }],
      cabinets: ["101", "202", "404"],
    }
  },


  mounted: function () {
    console.log(this.bron)
    // axios.get('/API/v1/reservations')
    //     .then(response => console.log(response.data))

    //this.bron.sort((a, b) => new Date(a.startTime).getTime() - new Date(b.startTime).getTime())
    this.bron.forEach(elem => {
      let t = new Date(elem.startTime)
      elem.day = t.getDay() + '.' + t.getMonth()
      console.log(t)
    })
    let temp = groupBy('day')
    console.log(temp)

    // console.log(this.bron)

    // this.bron.forEach(day => {
    //   day.cabinets.forEach(cabinet => {
    //     let reservedHours = cabinet.reserved
    //     cabinet.reserved = new Array(12)
    //     reservedHours.forEach(reservedHour => {
    //       cabinet.reserved[reservedHour.start.getHours() - 8] = reservedHour
    //     })
    //   })
    // })
  },

  methods: {

    getLength(val) {
      if (val) {
        //let t = new Date(val.end - val.start - 10800000)
        //return Math.trunc(((t.getHours() * 60) + t.getMinutes()) / 60 * 100) + t.getHours() + '%'
        return val.duration / 60 * 100 + Math.trunc(val.duration / 60 - 1) + '%'
      }
    },

    getLeft(val) {
      if (val) {
        return val.start.getMinutes() / 60 * 100 + '%'
        // return Math.trunc(val.duration / 60) / 60 * 100 + '%'
      }
    },

    thisDay(date) {
      let options = {month: 'long', day: 'numeric', year: 'numeric'}
      return date.toLocaleDateString("ru-RU", options)
      // return date
    }
  },

  computed: {}

}
</script>


<style>

#calendar {
  height: fit-content;
  width: 100%;
  /*overflow: auto;*/
}

.tab {
  height: 100%;
  width: 100%;
  /*padding-bottom: 30px;*/
  display: flex;
  margin-bottom: 30px;
}

.tab h3 {
  font-size: 20px;
  margin: 5px;
  transform: rotate(180deg);
  writing-mode: tb;
  text-align: center;
}

TABLE {
  border-collapse: collapse;
}

TD, TH, TD {
  border: 1px solid rgba(0, 0, 0, 0.25);
  padding: 0;
}

.cabinet {
  margin: auto;
  min-width: 75px;
  height: 45px;
  text-align: center;
  padding: 5px 0;
  font-size: 20px;
  font-weight: bold;
}


.rectangle {
  height: 55px;
  width: 0;
  /*background: rgba(77, 161, 247, 0.75);*/
  text-align: center;
  position: relative;
  overflow: hidden;
  text-shadow: 1px 1px 2px black;
  box-shadow: 1px 0.5px 2px #0005;
}

.rectangle p {
  position: absolute;
  margin: 1px;
  color: rgb(247 243 241);
  text-shadow: 1px 1px 2px black;
}

</style>
