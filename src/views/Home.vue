<template>
  <div class="home">
    <img src="HfGWortmarke.svg" class="logo" />
    <h2 class="header">talks</h2>
    <h2 class="header hd2">talks</h2>
    <!-- <h2 class="header hd3">talks</h2>-->
    <HelloWorld msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'

export default {
  name: 'Home',
  components: {
    HelloWorld
  }
}
</script>

<style scoped>
  .logo {
    position: absolute;
    top:90px;
    left:90px;
    width:220px;
  }

  .header {
    font-family: "Roboto";
    font-weight: 200;
    font-size: 18em;
    position: absolute;
    top:55vh;
    left:90px;
    color:#ffffff;
  }

  .hd2 {
    top:57vh;
    left:92px;
    color:#dfdfdf;
    z-index: -9000;
  }

  .hd3 {
    top:64vh;
    left:97px;
    color:#ababab;
    z-index: -9999;
  }
</style>