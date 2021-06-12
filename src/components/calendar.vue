<template>
  <div id="calendar">
    <div class="tab">
      <h3>1.06.2021</h3>
      <table style="width: inherit;">
        <time-line/>
        <tr
            v-for="(t, i) in bron"
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
import TimeLine from "@/components/timeLine";

export default {
  name: 'calendar',

  components: {
    TimeLine,
  },

  data() {
    return {
      bron: [
        {
          cabinet: '101',
          reserved: [
            {
              start: new Date('11.06.2021 12:00'),
              end: new Date('11.06.2021 13:00'),
              name: 'Залупа Залупа ',
              color: 'rgb(168 0 215 / 72%)'
            }, {
              start: new Date('11.06.2021 16:00'),
              end: new Date('11.06.2021 17:00'),
              name: 'Громындяй',
              color: 'rgb(70 100 227 / 72%)'
            }
          ],
        }, {
          cabinet: '202',
          reserved: [{
            start: new Date('11.06.2021 13:00'),
            end: new Date('11.06.2021 14:00'),
            name: 'Запупяй',
            color: 'rgb(177 0 55 / 71%)'
          }]
        }, {
          cabinet: '303',
          reserved: [{
            start: new Date('11.06.2021 9:30'),
            end: new Date('11.06.2021 10:30'),
            name: 'Контрациптяй',
            color: 'rgb(62 218 64 / 71%)'
          }]
        },
      ],
    }
  },


  mounted: function () {
    this.bron.forEach(el => {
      let ta = el.reserved
      el.reserved = new Array(12)
      ta.forEach(tael => el.reserved[tael.start.getHours() - 8] = tael)
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
  },

  computed: {}

}
</script>


<style>

#calendar {
  height: 100%;
  width: 100%;
  overflow: auto;
}

.tab {
  height: 100%;
  width: 100%;
  /*padding-bottom: 30px;*/
  display: flex;
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
}


.rectangle {
  height: 40px;
  width: 0;
  /*background: rgba(77, 161, 247, 0.75);*/
  text-align: center;
  position: relative;
  overflow: hidden;
}

.rectangle p {
  position: absolute;
  margin: 1px;
  color: rgb(247 243 241);
}

</style>
