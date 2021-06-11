<template>
  <div id="calendar">

    <p>1.06.2021</p>
    <table style="width: inherit;">
      <time-line/>
      <tr
          v-for="(t, i) in bron"
          :key="i"
      >
        <td class="cabinet">{{ t.cabinet }}</td>
        <td
            v-for="(g,j) in t.reserved"
            :key="j"
        >
          <div class="rectangle" :style="{width: getLength(g), left: getLeft(g)}"></div>
        </td>
      </tr>
    </table>
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
        {cabinet: '1', reserved: [{start: new Date('11.06.2021 12:00'), end: new Date('11.06.2021 16:00')}]},
        {cabinet: '2', reserved: [{start: new Date('11.06.2021 13:00'), end: new Date('11.06.2021 15:00')}]},
        {cabinet: '3', reserved: [{start: new Date('11.06.2021 9:30'), end: new Date('11.06.2021 12:30')}]},
      ],
    }
  },


  mounted: function () {
    this.bron.forEach(el => {
      let ta = el.reserved
      el.reserved = new Array(12)
      ta.forEach(tael => el.reserved[tael.start.getHours() - 8] = tael)
    })
    // console.log(this.bron)
  },

  methods: {
    getLength(val) {
      if (val) {
        let t = new Date(val.end - val.start - 10800000)
        // console.log('getHours:', t.getHours(), '; getMinutes:', t.getMinutes())
        // console.log((t.getHours() * 60 + t.getMinutes()) / 60 * 100 + '%')
        return Math.trunc(((t.getHours() * 60.75) + t.getMinutes()) / 60 * 100) + '%'
      }
    },

    getLeft(val) {
      if (val) {
        return val.start.getMinutes() / 60 * 100 + '%'
      }
    }
  }

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
  padding-bottom: 30px;
}

.tab p {
  font-size: 20px;
  margin: 5px;
}

TABLE {
  border-collapse: collapse;
}

TD, TH, TD {
  border: 1px solid rgba(0, 0, 0, 0.25);
  padding: 0;
}

br {
  height: 20px;
}

.rectangle {
  height: 20px;
  width: 0;
  background: rgba(77, 161, 247, 0.75);
  color: aliceblue;
  text-align: center;
  position: relative;
  /*left: 50%;*/
}

.cabinet {
  margin: 0;
  /*border: solid 1px;*/
  width: 75px;
  text-align: center;
  padding: 5px 0;
}

</style>
