<template>
  <div id="calendar">
    <div class="tab">
      <!--      {{ console.log(this.bron) }}-->
      <h3>{{ thisDay(bron[0].date) }}</h3>
      <table style="width: inherit;">
        <time-line/>
        <tr v-for="(t, i) in bron[0].cabinets" :key="i">
          <td class="cabinet">{{ cabinets[t.cabinetId] }}</td>
          <td
              v-for="(g, j) in t.reserved"
              :key="j"
          >
            <div v-if="getLength(g)">
              <div
                  class="rectangle"
                  :style="{width: getLength(g), left: getLeft(g), background: g.color}"
              ><p>{{ g.name }}</p></div>
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
              ><p>{{ g.name }}</p></div>
            </div>
          </td>
        </tr>
      </table>
    </div>
  </div>
</template>

<script>
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
      bron: [{
        date: new Date("10.27.2021"),
        cabinets: [
          {
            cabinetId: 0,
            reserved: [
              {
                start: new Date("1970-01-01 " + "11:00"),
                duration: 60,
                name: '11-60 ',
                color: 'rgb(168 0 215 / 72%)'
              },
              {
                start: new Date("1970-01-01 " + "12:00"),
                duration: 60,
                name: '12-60 ',
                color: 'rgb(0 46 215 / 72%)'
              }, {
                start: new Date("1970-01-01 " + "8:00"),
                duration: 120,
                name: '8-120',
                color: 'rgb(70 100 227 / 72%)'
              }
            ],
          }, {
            cabinetId: 1,
            reserved: [{
              start: new Date("1970-01-01 " + "13:00"),
              duration: 60,
              name: '13-60',
              color: 'rgb(177 0 55 / 71%)'
            }]
          }, {
            cabinetId: 2,
            reserved: [{
              start: new Date("1970-01-01 " + "14:00"),
              duration: 60,
              name: '14-60',
              color: 'rgb(62 218 64 / 71%)'
            }]
          },
        ]
      }, {
        date: new Date("10.28.2021"),
        cabinets: [
          {
            cabinetId: 0,
            reserved: [
              {
                start: new Date("1970-01-01 " + "9:00"),
                duration: 45,
                name: '9-45 ',
                color: 'rgb(168 0 215 / 72%)'
              },
              {
                start: new Date("1970-01-01 " + "8:30"),
                duration: 30,
                name: '8-30 ',
                color: 'rgb(0 46 215 / 72%)'
              }, {
                start: new Date("1970-01-01 " + "19:00"),
                duration: 60,
                name: '19-60',
                color: 'rgb(70 100 227 / 72%)'
              }
            ],
          }, {
            cabinetId: 1,
            reserved: [{
              start: new Date("1970-01-01 " + "11:15"),
              duration: 90,
              name: '11-90',
              color: 'rgb(177 0 55 / 71%)'
            }]
          }, {
            cabinetId: 2,
            reserved: [{
              start: new Date("1970-01-01 " + "14:00"),
              duration: 60,
              name: '14-60',
              color: 'rgb(62 218 64 / 71%)'
            }]
          },
        ]
      }, {
        date: new Date("10.29.2021"),
        cabinets: [
          {
            cabinetId: 0,
            reserved: [
              {
                start: new Date("1970-01-01 " + "12:00"),
                duration: 60,
                name: '12-60 ',
                color: 'rgb(168 0 215 / 72%)'
              },
              {
                start: new Date("1970-01-01 " + "9:00"),
                duration: 45,
                name: '9-45 ',
                color: 'rgb(0 46 215 / 72%)'
              }, {
                start: new Date("1970-01-01 " + "14:00"),
                duration: 90,
                name: '14-90',
                color: 'rgb(70 100 227 / 72%)'
              }
            ],
          }, {
            cabinetId: 1,
            reserved: [{
              start: new Date("1970-01-01 " + "12:00"),
              duration: 120,
              name: '12-120',
              color: 'rgb(177 0 55 / 71%)'
            }]
          }, {
            cabinetId: 2,
            reserved: [{
              start: new Date("1970-01-01 " + "8:00"),
              duration: 720,
              name: '17-60',
              color: 'rgb(62 218 64 / 71%)'
            }]
          },
        ]
      }],

      cabinets: ["101", "202", "404"],
    }
  },


  mounted: function () {
    this.bron.forEach(day => {
      day.cabinets.forEach(cabinet => {
        let ta = cabinet.reserved
        cabinet.reserved = new Array(12)
        ta.forEach(tael => cabinet.reserved[tael.start.getHours() - 8] = tael)
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
}

.rectangle p {
  position: absolute;
  margin: 1px;
  color: rgb(247 243 241);
  text-shadow: 1px 1px 2px black;
}

</style>
