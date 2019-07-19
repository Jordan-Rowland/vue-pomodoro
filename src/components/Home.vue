<template>
  <div class="container">
<!--     <countdown
    :workTimeProp="workTimeData"
    :restTimeProp="restTimeData"
    :roundsProp="roundsData"/> -->
    <PSetup @emitUp="dataToCountdown"/>
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

  const activeComponent = 'PSetup';

  const workTimeData = value();
  const restTimeData = value();
  const roundsData = value();

  const dataToCountdown = (info) => {
    workTimeData.value = info.work;
    restTimeData.value = info.rest;
    roundsData.value = info.rounds;
    activeComponent.value = 'Countdown';
  };

  return {
    activeComponent,
    workTimeData,
    restTimeData,
    roundsData,
    dataToCountdown,
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
