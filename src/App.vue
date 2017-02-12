<template>
  <div id="app">
  	<bundle-list></bundle-list>
    <software-list></software-list>
  </div>
</template>

<style lang="scss">
  @import url(//db.onlinewebfonts.com/c/9126c154a82d08fe6124045ce0fc61d9?family=AlmaqW01-Refined);

  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }

  html {
    background-color: #141a1e;
  }

  p {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
  }

  a {
    text-decoration: none;
    color: #2c3e50;
  }

  h1, h2 {
    font-family: 'AlmaqW01-Refined', 'Avenir', Helvetica, Arial, sans-serif;
    font-weight: 500;
  }

  ul {
    list-style-type: none;
  }

</style>

<script>
import SoftwareList from './components/SoftwareList.vue'
import BundleList from './components/BundleList.vue'

export default {
  name: 'app',
  components: {
    SoftwareList,
    BundleList
  }
}
</script>
