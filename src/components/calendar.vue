<template>
  <div id="calendar">
    <div class="tab">
      <h3>{{ thisDay(bron[0].date) }}</h3>
      <table style="width: inherit;">
        <time-line/>
        <tr
            v-for="(t, i) in bron[0].cabinets"
            :key="i"
        >
          <td class="cabinet">{{ cabinets[t.cabinetId] }}</td>
          <td
              v-for="(g, j) in t.reserved"
              :key="j"
          >
            <div v-if="getLength(g)">
              <div
                  class="rectangle"
                  :style="{width: getLength(g), left: getLeft(g), background: g.color}"
              >
                <p>{{ g.title }}</p>
<!--                <p :style="{top: 15}">{{ g.clientName }}</p>-->
              </div>
            </div>
          </td>
        </tr>
      </table>
    </div>
    <div
        class="tab"
        v-for="(ttt, ti) in bron.slice().slice(1)"
        :key="ti"
    >
      <h3>{{ thisDay(ttt.date) }}</h3>
      <table style="width: inherit;">
        <hours/>
        <tr
            v-for="(t, i) in ttt.cabinets"
            :key="i"
        >
          <td class="cabinet">{{ cabinets[t.cabinetId] }}</td>
          <td
              v-for="(g, j) in t.reserved"
              :key="j"
          >
            <div v-if="getLength(g)">
              <div
                  class="rectangle"
                  :style="{width: getLength(g), left: getLeft(g), background: g.color}"
              >
                <p>{{ g.title }}</p>
<!--                <p :style="{top: 15}">{{ g.clientName }}</p>-->
              </div>
            </div>
          </td>
        </tr>
      </table>
    </div>
  </div>
</template>

<script>

import axios from "axios";
import timeLine from "./timeLine";
import hours from "./hours";

export default {
  name: 'calendar',


  components: {
    timeLine,
    hours,
  },


  data() {
    return {
      bron: [],
      cabinets: ["", "501", "506", "2 аккаунт"],
      timeLine: {Transform: 1, top: 1}
    }
  },


  mounted: async function () {
    await axios.get('/API/v1/reservations')
        .then(response => {
          this.bron = response.data
        })

    this.bron.forEach(day => {
      day.date = new Date(day.date)
      day.cabinets.forEach(cabinet => {
        let cabinetsReserved = cabinet.reserved
        cabinet.reserved = new Array(12)
        cabinetsReserved.forEach(reservation => {
          reservation.startTime = new Date(reservation.startTime - 10800000)
          reservation.color = 'rgb(' + reservation.color + ' / 72%)'
          cabinet.reserved[reservation.startTime.getHours() - 8] = reservation
        })
      })
    })
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
        return val.startTime.getMinutes() / 60 * 100 + '%'
        // return Math.trunc(val.duration / 60) / 60 * 100 + '%'
      }
    },

    thisDay(date) {
      let options = {month: 'long', day: 'numeric', year: 'numeric', weekday: 'narrow'}
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
  display: flex;
  margin-bottom: 30px;
  flex-direction: column;
}

.tab h3 {
  font-size: 20px;
  margin: 5px;
  /* transform: rotate(180deg); */
  -ms-writing-mode: tb;
  /* writing-mode: tb; */
  /* text-align: center; */
}

TABLE {
  border-collapse: collapse;
  width: inherit;
  height: fit-content;
}

TD, TH, TD {
  border: 1px solid rgba(0, 0, 0, 0.25);
  padding: 0;
}

.cabinet {
  margin: auto;
  min-width: 75px;
  height: 55px;
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
  margin-left: 5px;
  color: rgb(247 243 241);
  text-shadow: 1px 1px 2px black;
  font-size: 13px;
}

</style>
