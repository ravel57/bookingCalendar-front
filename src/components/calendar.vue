<template>
  <div id="calendar">
    <div class="tab">
      <h3>{{ thisDay(bron[0].date) }}</h3>
      <table style="width: inherit;">
        <time-line/>
        <tr v-for="(t, i) in bron[0].cabinets" :key="i">
          <td class="cabinet">{{ t.cabinet }}</td>
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
          <td class="cabinet">{{ t.cabinet }}</td>
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
        date: new Date('06.12.2021'),
        cabinets: [
          {
            cabinet: '101',
            reserved: [
              {
                start: new Date('11.06.2021 12:00'),
                end: new Date('11.06.2021 13:00'),
                name: 'Name_1 ',
                color: 'rgb(168 0 215 / 72%)'
              },
              {
                start: new Date('11.06.2021 13:00'),
                end: new Date('11.06.2021 16:00'),
                name: 'Name_5 ',
                color: 'rgb(0 46 215 / 72%)'
              }, {
                start: new Date('11.06.2021 16:00'),
                end: new Date('11.06.2021 17:00'),
                name: 'Name_2 Name_2',
                color: 'rgb(70 100 227 / 72%)'
              }
            ],
          }, {
            cabinet: '202',
            reserved: [{
              start: new Date('11.06.2021 13:00'),
              end: new Date('11.06.2021 14:00'),
              name: 'Name_3',
              color: 'rgb(177 0 55 / 71%)'
            }]
          }, {
            cabinet: '303',
            reserved: [{
              start: new Date('11.06.2021 9:30'),
              end: new Date('11.06.2021 10:30'),
              name: 'Name_4',
              color: 'rgb(62 218 64 / 71%)'
            }]
          },
        ]
      },{
        date: new Date('06.12.2021'),
        cabinets: [
          {
            cabinet: '101',
            reserved: [
              {
                start: new Date('11.06.2021 12:00'),
                end: new Date('11.06.2021 13:00'),
                name: 'Name_1 ',
                color: 'rgb(168 0 215 / 72%)'
              },
              {
                start: new Date('11.06.2021 13:00'),
                end: new Date('11.06.2021 16:00'),
                name: 'Name_5 ',
                color: 'rgb(0 46 215 / 72%)'
              }, {
                start: new Date('11.06.2021 16:00'),
                end: new Date('11.06.2021 17:00'),
                name: 'Name_2 Name_2',
                color: 'rgb(70 100 227 / 72%)'
              }
            ],
          }, {
            cabinet: '202',
            reserved: [{
              start: new Date('11.06.2021 13:00'),
              end: new Date('11.06.2021 14:00'),
              name: 'Name_3',
              color: 'rgb(177 0 55 / 71%)'
            }]
          }, {
            cabinet: '303',
            reserved: [{
              start: new Date('11.06.2021 9:30'),
              end: new Date('11.06.2021 10:30'),
              name: 'Name_4',
              color: 'rgb(62 218 64 / 71%)'
            }]
          },
        ]
      },{
        date: new Date('06.12.2021'),
        cabinets: [
          {
            cabinet: '101',
            reserved: [
              {
                start: new Date('11.06.2021 12:00'),
                end: new Date('11.06.2021 13:00'),
                name: 'Name_1 ',
                color: 'rgb(168 0 215 / 72%)'
              },
              {
                start: new Date('11.06.2021 13:00'),
                end: new Date('11.06.2021 16:00'),
                name: 'Name_5 ',
                color: 'rgb(0 46 215 / 72%)'
              }, {
                start: new Date('11.06.2021 16:00'),
                end: new Date('11.06.2021 17:00'),
                name: 'Name_2 Name_2',
                color: 'rgb(70 100 227 / 72%)'
              }
            ],
          }, {
            cabinet: '202',
            reserved: [{
              start: new Date('11.06.2021 13:00'),
              end: new Date('11.06.2021 14:00'),
              name: 'Name_3',
              color: 'rgb(177 0 55 / 71%)'
            }]
          }, {
            cabinet: '303',
            reserved: [{
              start: new Date('11.06.2021 9:30'),
              end: new Date('11.06.2021 10:30'),
              name: 'Name_4',
              color: 'rgb(62 218 64 / 71%)'
            }]
          },
        ]
      },{
        date: new Date('06.12.2021'),
        cabinets: [
          {
            cabinet: '101',
            reserved: [
              {
                start: new Date('11.06.2021 12:00'),
                end: new Date('11.06.2021 13:00'),
                name: 'Name_1 ',
                color: 'rgb(168 0 215 / 72%)'
              },
              {
                start: new Date('11.06.2021 13:00'),
                end: new Date('11.06.2021 16:00'),
                name: 'Name_5 ',
                color: 'rgb(0 46 215 / 72%)'
              }, {
                start: new Date('11.06.2021 16:00'),
                end: new Date('11.06.2021 17:00'),
                name: 'Name_2 Name_2',
                color: 'rgb(70 100 227 / 72%)'
              }
            ],
          }, {
            cabinet: '202',
            reserved: [{
              start: new Date('11.06.2021 13:00'),
              end: new Date('11.06.2021 14:00'),
              name: 'Name_3',
              color: 'rgb(177 0 55 / 71%)'
            }]
          }, {
            cabinet: '303',
            reserved: [{
              start: new Date('11.06.2021 9:30'),
              end: new Date('11.06.2021 10:30'),
              name: 'Name_4',
              color: 'rgb(62 218 64 / 71%)'
            }]
          },
        ]
      }, {
        date: new Date('06.13.2021'),
        cabinets: [
          {
            cabinet: '101',
            reserved: [
              {
                start: new Date('11.06.2021 10:00'),
                end: new Date('11.06.2021 11:30'),
                name: 'Name_1 ',
                color: 'rgb(0 175 215 / 72%)'
              }, {
                start: new Date('11.06.2021 16:00'),
                end: new Date('11.06.2021 17:00'),
                name: 'Name_2 Name_2',
                color: 'rgb(215 119 0 / 72%)'
              }
            ],
          }, {
            cabinet: '202',
            reserved: [{
              start: new Date('11.06.2021 13:00'),
              end: new Date('11.06.2021 14:00'),
              name: 'Name_3',
              color: 'rgb(0 177 63 / 71%)'
            }, {
              start: new Date('11.06.2021 16:30'),
              end: new Date('11.06.2021 17:30'),
              name: 'Name_6',
              color: 'rgb(177 0 55 / 71%)'
            }]
          }, {
            cabinet: '303',
            reserved: [{
              start: new Date('11.06.2021 12:30'),
              end: new Date('11.06.2021 14:30'),
              name: 'Name_4',
              color: 'rgb(62 218 64 / 71%)'
            }]
          },
        ]
      }, {
        date: new Date('06.14.2021'),
        cabinets: [
          {
            cabinet: '101',
            reserved: [
              {
                start: new Date('11.06.2021 10:00'),
                end: new Date('11.06.2021 11:30'),
                name: 'Name_1 ',
                color: 'rgb(0 175 215 / 72%)'
              }, {
                start: new Date('11.06.2021 16:00'),
                end: new Date('11.06.2021 17:00'),
                name: 'Name_2 Name_2',
                color: 'rgb(215 119 0 / 72%)'
              }
            ],
          }, {
            cabinet: '202',
            reserved: [{
              start: new Date('11.06.2021 13:00'),
              end: new Date('11.06.2021 14:00'),
              name: 'Name_3',
              color: 'rgb(0 177 63 / 71%)'
            }, {
              start: new Date('11.06.2021 16:30'),
              end: new Date('11.06.2021 17:30'),
              name: 'Name_6',
              color: 'rgb(177 0 55 / 71%)'
            }]
          }, {
            cabinet: '303',
            reserved: [{
              start: new Date('11.06.2021 12:30'),
              end: new Date('11.06.2021 14:30'),
              name: 'Name_4',
              color: 'rgb(62 218 64 / 71%)'
            }]
          },
        ]
      },],
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
        let t = new Date(val.end - val.start - 10800000)
        return Math.trunc(((t.getHours() * 60) + t.getMinutes()) / 60 * 100) + t.getHours() + '%'
      }
    },

    getLeft(val) {
      if (val) {
        return val.start.getMinutes() / 60 * 100 + '%'
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
  height: 100%;
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
