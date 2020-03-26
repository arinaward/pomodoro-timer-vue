<template>
  <div class="timer">
    <span class="time">{{ formattedTimeLeft }}</span>
  </div>
</template>

<script>
export default {
  props: {
    timeLeft: {}
  },
  computed: {
    formattedTimeLeft() {
      const timeLeft = this.timeLeft;
      let minutes = Math.floor(timeLeft / 60);
      let seconds = timeLeft % 60;

      minutes = minutes < 10 ? "0" + minutes : minutes;
      seconds = seconds < 10 ? "0" + seconds : seconds;

      return `${minutes}:${seconds}`;
    }
  },
  methods: {
    playSound() {
      let audio = new Audio(require("../../assets/computer-magic.mp3"));
      audio.play();
    }
  }
};
</script>

<style scoped>
.timer {
  font-size: 33px;
  position: absolute;
  margin-top: 145px;
  width: 100%;
  height: 100%;
  display: none;
}
.visible {
  display: inline-block;
}
</style>
