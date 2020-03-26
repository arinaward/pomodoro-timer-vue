<template>
  <div class="circle-element">
    <div class="circle">
      <svg
        width="200"
        height="200"
        viewBox="0 0 100 100"
        fill="none"
        xmlns="http://www.w3.org/2000/svg"
      >
        <g>
          <circle id="background" cx="50" cy="50" r="50" fill="#C4C4C4" />
          <circle
            id="segment"
            cx="50"
            cy="50"
            r="47.5"
            fill="none"
            stroke="#ce4b99"
            stroke-width="5"
            :stroke-dasharray="animateRing"
          />
          <circle id="overlay" cx="50" cy="50" r="45" fill="#F4F4F4" />
        </g>
      </svg>
    </div>
    <div class="content">
      <slot></slot>
    </div>
  </div>
</template>

<style>
.circle {
  position: relative;
  z-index: -1;
}
.content {
  position: absolute;
  width: 100%;
  height: 100%;
  z-index: 0;
  margin-top: -140px;
  margin-left: 10px;
}
#segment {
  stroke: #ff1a1ab6;
  stroke-linecap: round;
  transform: rotate(90deg);
  transform-origin: center;
  transition: 1s linear all;
}
#overlay {
  fill: #ffffff;
}
svg {
  transform: scaleY(-1);
}
</style>

<script>
const FULL_DASH_ARRAY = 298;

export default {
  props: {
    timeLeft: {},
    workPeriod: {},
  },
  computed: {
    timeFraction() {
      const rawTimeFraction = this.timeLeft / this.workPeriod;
      return rawTimeFraction - (1 / this.workPeriod) * (1 - rawTimeFraction);
    },
     animateRing() {
      return `${(this.timeFraction * FULL_DASH_ARRAY).toFixed(2)} ${FULL_DASH_ARRAY}`;
    },
  },
};
</script>