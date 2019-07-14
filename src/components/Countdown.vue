<template>
  <div id="main">
    <div class="buttons">
      <app-button
        text="Add Round"
        @click.native="rounds++">
      </app-button>
      <app-button
        @click.native="rounds--"
        text="Skip Round">
      </app-button>
      <app-button
        @click.native=""
        text="End">
      </app-button>
    </div>
    <div class="mode">
      <p v-if="workMode" class="work-mode">Work</p>
      <p v-else>Rest</p>
      <p id="timer">3:30</p>
    </div>
    <div class="details">
      <em>Rest: {{ restTime }} mins</em> <br>
      <em>Rounds: {{ rounds }}</em> <br>
      <em>Total time: {{workTime + restTime}} mins</em>
    </div>
  </div>
</template>

<script>
/* jshint esversion: 9 */
import { value } from 'vue-function-api';
import AppButton from './AppButton.vue';

export default {
name: 'Countdown',
setup() {
  const workMode = value(true);
  const workTime = value(25);
  const restTime = value(5);
  const rounds = value(5);

  // const click = () => console.log('clicked');

  return {
    workMode,
    workTime,
    restTime,
    rounds,


    // click,
  };
},
components: {
  'app-button': AppButton,
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

.mode {
  text-align: center;
}

.work-mode {
  font-size: 2em;
}

#timer {
  font-size: 4em;
  position: relative;
  top: -50px;
}

.buttons {
  display: flex;
  justify-content: center;
}

.details {
  position: absolute;
  font-size: 1.3em;
  top: 250px;
}
</style>
