<template>
  <div class="graphs">
    <div class="graph">
      <div class="bar-wrap" v-for="timer in timers" :key="timer._id">
        <p class="bar-title">{{timer.title}}</p>
        <div
          class="bar"
          v-bind:style="{ width: timerWidthsNormalized[timer._id] + '%' }"
        >
          <p class="bar-time">{{Math.round(timer.time * 100) / 100}} min</p>
        </div>
      </div>
    </div>
    <Footer />
  </div>
</template>

<script>

import Footer from '../components/Footer.vue';
export default {
  name: "Graphs",
  created() {
    this.getTimerWidths();
  },
  data() {
    return {
      timers: [
        {
          title: "Phil 110",
          active: false,
          time: 25,
          _id: 0
        },
        {
          title: "Stat 240",
          active: false,
          time: 45,
          _id: 1
        },
        {
          title: "CS 260",
          active: false,
          time: 354,
          _id: 2
        },
        {
          title: "CS 340",
          active: false,
          time: 800,
          _id: 3
        },
        {
          title: "CS 330",
          active: false,
          time: 244,
          _id: 4
        },
        {
          title: "CS 404",
          active: false,
          time: 140,
          _id: 5
        }
      ],
      timerWidthsNormalized: {},
    };
  },

  methods: {
    getTimerWidths() {
      let times = this.timers.map((timer) => {
        return timer.time;
      });
      console.log(times);
      let max = Math.max(...times);
      let min = Math.min(...times);
      let maxMinusMin = max - min;
      console.log(max);
      console.log(min);
      console.log(maxMinusMin);

      for (let i = 0; i < times.length; i++) {
        console.log(times.length);
        if (maxMinusMin == 0) {
          console.log(this.timers[i]._id);
          this.timerWidthsNormalized[this.timers[i]._id] = 100;
        } else if (times[i] == max) {
          this.timerWidthsNormalized[this.timers[i]._id] = 100;
        } else {
          this.timerWidthsNormalized[this.timers[i]._id] =
            (times[i] / max) * 100;
        }
      }
    },
  },
  components: {
    Footer
  },
};
</script>

<style scoped>
.graph {
  width: 90%;
  margin: 0 auto;
  margin-bottom: 20px;
  padding: 5px;
  border: 2px solid #ce3d35;
}

.bar-wrap {
  margin-bottom: 10px;
}

.bar-title {
  width: fit-content;
}

.bar {
  height: 50px;
  background-color: #5daa5d;
  display: grid;
  align-items: center;
  justify-items: right;
}

.bar-time {
  width: fit-content;
  margin-right: 5px;
}
</style>
