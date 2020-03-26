<template>
  <div id="app">
    <div id="container">
      <p>Pomodoro timer</p>
      <CountdownTimer :time-left="timeLeft" :class="{ visible: active }" ref="countdownTimer" />
      <ProgressRing :time-left="timeLeft" :work-period="workPeriod">
        <PlayButton
          @click="handleStart(), (active = !active)"
          :class="{ active: !active }"
        />
      </ProgressRing>
      <p class="message" v-if="active">
        Have a productive time, my friend!
      </p>
    </div>
  </div>
</template>

<script>
import ProgressRing from "./components/ProgressRing";
import CountdownTimer from "./components/CountdownTimer";
import PlayButton from "./components/PlayButton";

export default {
  name: "App",
  components: {
    ProgressRing,
    CountdownTimer,
    PlayButton
  },
  data() {
    return {
      workPeriod: 1500, // Time in seconds
      timePassed: 0,
      active: false
    };
  },
  computed: {
    timeLeft() {
      return this.active ? this.workPeriod - this.timePassed : 0;
    }
  },
  methods: {
    handleStart() {
      this.startTimer();
    },
    startTimer() {
      const start = Date.now();
      let tickInterval = setInterval(tick.bind(this), 500);

      function tick() {
        if (this.timeLeft > 0) {
          this.timePassed = Math.floor((Date.now() - start) / 1000);
        } else {
          clearInterval(tickInterval);
          this.active = false;
          this.timePassed = 0;
          this.$refs.countdownTimer.playSound();
        }
      }
    }
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
#container {
  position: relative;
  display: flex;
  flex-direction: column;
  justify-content: center;
}
p {
  font-size: 20px;
}
</style>
