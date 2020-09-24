<template>
  <div class="content">
    <ul class="timer-list">
      <Timer v-for="timer in timers" :key="timer.id" :timer="timer" />
      <li class="add-timer" @click="this.addTimer">
        <div>+</div>
      </li>
    </ul>
  </div>
</template>

<script>
import Timer from "./Timer";
export default {
  name: "TimersList",
  components: {
    Timer,
  },
  mounted() {
    // if (type === "seconds") return time - minutes * 60;;
    // if (type === "minutes") return Math.floor(this.count / 60);;
    // if (type === "hours") return ` :${this.count}`;

    var num = this.count;
    var hours = num / 60;
    var rhours = Math.floor(hours);
    var minutes = (hours - rhours) * 60;
    var rminutes = Math.round(minutes);
    return (
      num + " minutes = " + rhours + " hour(s) and " + rminutes + " minute(s)."
    );
  },
  data() {
    return {
      timers: [
        { id: 1, timerCount: 0, time: "seconds" },
        { id: 2, timerCount: 0, time: "minutes" },
        { id: 3, timerCount: 0, time: "hours" },
      ],
    };
  },
  methods: {
    addTimer() {
      this.timers = [
        ...this.timers,
        {
          timerCount: 0,
          id: Date.now(),
        },
      ];
    },
  },
};
</script>

<style scoped>
ul {
  margin: 0;
  padding: 0;
}
.content {
  margin: auto;
}

@media (max-width: 1132) {
  .content {
    width: 80%;
  }
}

.timer-list {
  display: flex;
  align-items: center;
  list-style: none;
  flex-wrap: wrap;
}

.add-timer {
  max-width: 225px;
  width: 100%;
  display: flex;
  height: 120px;
  cursor: pointer;
  background-color: rgba(105, 105, 105, 1);
  color: #9e9e9e;
}
.add-timer div {
  font-size: 32px;
  font-weight: 400;
  margin: auto;
}

@media (min-width: 768px) {
  .content {
    width: 78%;
  }
  li {
    margin-bottom: 50px;
  }
  li {
    margin-left: 50px;
  }
}

@media (max-width: 768px) {
  .timer {
    margin-bottom: 50px;
  }
  .timer-list {
    flex-direction: column;
    margin-bottom: 30px;
  }
  .content {
    width: 82%;
    padding-top: 30px;
  }
}
</style>