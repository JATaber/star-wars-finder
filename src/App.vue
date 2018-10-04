<template>
  <div id="app">
    <Header></Header>
    <router-view/>
  </div>
</template>

<script>
import Header from './views/Header'

export default {
  name: 'App',
  components: {
    Header
  }
}
</script>

<style lang="scss" rel="stylesheet/scss">
body{
  background-color: black;
}

</style>