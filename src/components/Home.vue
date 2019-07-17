<template>
  <div class="container">
    <countdown
    :workTimeProp="5"
    :restTimeProp="2"
    :roundsProp="3"/>
    <PSetup/>
  </div>
</template>

<script>
/* jshint esversion: 9 */
import Countdown from './Countdown.vue';
import PSetup from './PSetup.vue';
import { value } from 'vue-function-api';

export default {
name: 'home',
setup() {

  return {

  };
},
components: {
  Countdown,
  PSetup,
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
  margin: 1rem;
}

.container {
  max-width: 80%;
  margin: auto;
}

/* Play with size when server is on, fag */

@media only screen and (min-width: 800px) {
  .container {
    max-width: 40rem;
  }
}

</style>
