<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <p>{{text}}</p>
  </div>
</template>

<script>

export default {
  name: 'App',
  data () {
    return {
      text: "hola"
    }
  },
  components: {
  }
}
</script>

<style lang="stylus">
#app
  font-family Avenir, Helvetica, Arial, sans-serif
  -webkit-font-smoothing antialiased
  -moz-osx-font-smoothing grayscale
  text-align center
  color #2c3e50
  margin-top 60px
</style>
