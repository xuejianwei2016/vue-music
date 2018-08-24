<template>
  <div id="app">
    <MHeader></MHeader>
    <Tab></Tab>
    <router-view/>
  </div>
</template>
 
<script>
import MHeader from "components/m-header/m-header.vue";
import Tab from "components/tab/tab.vue";

export default {
  name: "App",
  components: { MHeader, Tab }
};
</script>

<style style lang="stylus">
@import './common/stylus/variable.styl';
body {
  margin: 0;
  color: $color-theme;
  background: $color-background;
}

#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
}
</style>
