<template>
  <div id="app">
    <TimersList />
  </div>
</template>

<script>
import TimersList from "./components/TimersList";

export default {
  name: "App",
  components: {
    TimersList,
  },
};
</script>

<style>
* {
  box-sizing: border-box;
}
body {
  margin: 0;
  padding: 0;
  height: 100vh;
  background-color: rgba(53, 54, 56, 1);
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  width: 100%;
  display: flex;
  height: 100vh;
}
</style>
