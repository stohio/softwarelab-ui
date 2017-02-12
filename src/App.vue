<template>
  <div id="app">
  	<h1 class="logo">The Software Lab</h1>
  	<bundle-list></bundle-list>
    <software-list></software-list>
  </div>
</template>

<style lang="scss">
  @import url(//db.onlinewebfonts.com/c/9126c154a82d08fe6124045ce0fc61d9?family=AlmaqW01-Refined);

  $gray: #1e262c;
  $yellow: #f6c435;
  $orange: #e16622;
  $red: #d11d29;
  $purple: #542437;
  $blue: #3a5255;

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

  h1 {
  	font-size: 4rem;
  }

  h1, h2 {
    font-family: 'AlmaqW01-Refined', 'Avenir', Helvetica, Arial, sans-serif;
    font-weight: 500;
  }

  ul {
    list-style-type: none;
  }

  .logo {
  	position: absolute;
  	top: 0;
  	right: 0;
  	width: 100%;
  	text-align: right;
  	padding-right: 20px;
  	color: #222;
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
