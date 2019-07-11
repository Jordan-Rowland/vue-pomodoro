<template>
  <section class="section">
    <div class="container is-fluid">
      <div class="columns is-centered">
        <div class="column is-half">
          <countdown/>
        </div>
        <!-- <div class="columns">
          <div class="column box"></div>
          <div class="column box"></div>
          <div class="column box"></div>
        </div> -->
      </div>
      </div>
  </section>
</template>

<script>
/* jshint esversion: 9 */
import Countdown from './Countdown.vue';
import PSetup from './PSetup.vue';
import { value, computed } from 'vue-function-api';

export default {
  name: 'home',
  setup() {

    return {

    };
  },
  components: {
    Countdown,
  },

};
</script>

<style scoped>
#main {
  border: 2.3px black solid;
  border-radius: 12px;
  height: 300px;
  padding: 20px;
  position: relative;
}

div {
  margin: 15px;
}

.box {
  height: 100px;
  width: 100px;
  background-color: green;
}
</style>
