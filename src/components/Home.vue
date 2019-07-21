<template>
  <div>
    <header>
      Pomodoro Timer
    </header>
    <div class="container">
      <transition name="pulse" mode="out-in">
        <component :is="activeComponent"
        :workTimeProp="workTimeData"
        :restTimeProp="restTimeData"
        :roundsProp="roundsData"
        @emitUp="toCountdown"
        @emitEndRounds="toSetup"
        ></component>
      </transition>
    </div>
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

  const activeComponent = value('PSetup');

  const workTimeData = value();
  const restTimeData = value();
  const roundsData = value();

  const toCountdown = (info) => {
    workTimeData.value = Number(info.work);
    restTimeData.value = Number(info.rest);
    roundsData.value = Number(info.rounds);
    activeComponent.value = 'Countdown';
  };

  const toSetup = () => {
    activeComponent.value = 'PSetup';
  };

  return {
    activeComponent,
    workTimeData,
    restTimeData,
    roundsData,
    toCountdown,
    toSetup,
  };

},
components: {
  Countdown,
  PSetup,
},

};
</script>

<style scoped>
header {
  background-color: #5FBA7D;
  height: 6rem;
  width: 100%;
  margin-bottom: 50px;
  color: white;
  font-size: 2rem;
  display: flex;
  align-items: center;
  justify-content: center;
  font-weight: 700;
}

#main {
  border: .1rem #abc solid;
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

@media only screen and (max-width: 599px) {
  .container, header {
    min-width: 25rem;
  }
}

/* Animation 'pulse' */
.pulse-enter {
  opacity: 0;
  transform: rotateY(90deg);
}
.pulse-enter-active {
  transition: all .9s cubic-bezier(0.55, 0.085, 0.68, 0.53);
}
.pulse-leave {
  transform: scaleX(0) translateZ(0);
  opacity: 0;
}
.pulse-leave-active {
  transition: all .25s cubic-bezier(0.25, 0.46, 0.45, 0.94);
}

</style>
