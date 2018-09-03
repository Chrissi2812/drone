<template>
  <div id="app">
    <DroneList></DroneList>
    <Map></Map>
  </div>
</template>

<script>
import DroneList from './components/DroneList.vue';
import Map from './components/Map.vue';

export default {
  name: 'app',
  components: {
    DroneList,
    Map,
  },
};
</script>


<style lang="scss">
  // First, set the value for variable
  $mdc-typography-font-family: "Roboto", monospace;

  // Then, import required files
  @import "@material/typography/mixins";

  html {
    width: 100%;
    height: 100%;
  }

  body {
    @include mdc-typography(body2);

    width: 100%;
    min-height: 100%;
    margin: 0;
  }

  #app {
    display: grid;
    grid-template-columns: min-content 1fr;
    grid-template-rows: 1fr;
    height: 100%;
    width: 100%;
    position: absolute;
    top: 0;
    left: 0;
  }
</style>
