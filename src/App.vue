<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png" />
    <counter-cmp></counter-cmp>
  </div>
</template>

<script>
import CounterCmp from "@/components/Counter";
export default {
  name: "App",
  components: {
    CounterCmp,
  },
  data() {
    return {
      text: "hola",
    };
  },
};
</script>

<style lang="stylus">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
