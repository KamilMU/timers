<template>
  <li class="timer">
    <div class="timer-content" v-bind:style="{opacity: clickedPlay ? '1' : '0.5'}">
      <div class="timer__count" v-if="!calcTime()">{{ count }}</div>
      <div class="timer__count" v-if="calcTime() && !formatted">
        {{ count }}
      </div>
      <div class="timer__count" v-if="typeof count !== Number">
        {{ formatted }}
      </div>
      <div class="timer__btns">
        <div
          class="btn play"
          @click="this.increaseCount"
          v-if="clickedPlay === false"
        ></div>
        <div
          class="btn pause"
          @click="this.pauseCount"
          v-if="clickedPlay === true"
        ></div>
        <div class="btn stop" @click="this.stopCount"></div>
      </div>
    </div>
  </li>
</template>

<script>
export default {
  name: "Timer",
  props: ["timer"],
  data() {
    return {
      count: this.timer.timerCount,
      interval: null,
      formatted: "",
      isPaused: false,
      clickedPlay: false,
    };
  },
  methods: {
    increaseCount() {
      this.isPaused = false;
      this.clickedPlay = true;
      if (!this.isPaused) {
        this.interval = setInterval(() => {
          this.count++;
        }, 1000);
      }
    },
    stopCount() {
      this.count = 0;
      this.clickedPlay = false;
      this.formatted = "";
      clearInterval(this.interval);
    },
    pauseCount() {
      this.isPaused = true;
      this.clickedPlay = false;
      clearInterval(this.interval);
    },
    calcTime() {
      let hours = Math.floor(this.count / 60 / 60);
      let minutes = Math.floor(this.count / 60) - hours * 60;
      let seconds = this.count % 60;
      let formatted = `${minutes} : ${seconds}`;
      if (this.count > 60 && this.count < 3600)
        return (this.formatted = formatted);
      if (this.count < 60) return (this.count = seconds);
      if (this.count > 3600)
        return (this.formatted = hours + ":" + minutes + ":" + seconds);
      return this.count;
    },
  },
};
</script>

<style scoped>
button {
  cursor: pointer;
  padding: 10px 20px;
}

.timer {
  background-color: rgba(105, 105, 105, 1);
  text-align: center;
  color: #FFF;
  position: relative;
  width: 100%;
  padding: 22px 75px;
  font-size: 22px;
  font-weight: 400;
  height: 120px;
  max-width: 225px;
}

.timer-content {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  height: 100%;
}

@media (min-width: 768px) {
  /* li {
    margin-right: 50px;
  }
  li + li {
    margin-top: 50px;
  } */
}

@media (max-width: 768px) {
  /* li + li {
    margin-top: 50px;
  } */
}

.timer__count::after {
  content: "";
  position: absolute;
  top: 55px;
  bottom: 0;
  left: 0;
  right: 0;
  height: 0.5em;
  border-top: 1px solid rgba(158, 158, 158, 1);
}

.timer__btns {
  display: flex;
  width: 100%;
  justify-content: space-between;
}

.btn {
  cursor: pointer;
}

.play {
  width: 17px;
  border-top: 8px solid transparent;
  border-left: 12px solid #fff;
  border-bottom: 8px solid transparent;
  width: 0;
  content: "";
  display: inline-block;
  position: relative;
  border-style: solid;
  border-width: 10px 0 10px 20px;
  border-color: transparent transparent transparent white;
}

.pause {
  width: 10px;
  height: 20px;
  border-right: 4px solid #fff;
  border-left: 4px solid #fff;
}

.stop {
  width: 20px;
  height: 20px;
  background-color: #fff;
}
</style>