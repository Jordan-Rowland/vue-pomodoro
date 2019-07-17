<template>
  <div id="main">
    Work duration(minutes):
     <br> <input type="text" v-model="info.work"> <br>
    Rest duration(minutes):
     <br> <input type="text" v-model="info.rest"> <br>
    Rounds:
     <br> <input type="number" v-model="info.rounds">
     <app-button
      @click="startCountdown"
      id="start-button">
      Start!
     </app-button>
  </div>
</template>

<script>
/* jshint esversion: 9 */
import { value, state } from 'vue-function-api';
import AppButton from './AppButton.vue';

export default {
name: 'PSetup',
setup(props, context) {

  const info = state({
    work: number,
    rest: number,
    rounds: number,
  });

  const startCountdown = () => {
    // emit up to parent to pass to countdown component
    constext.emit();
  };

  return {

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
  display: flex;
  align-items: center;
  justify-content: space-around;
  flex-direction: column;
}

#start-button {
  margin-top: 1rem;
}

</style>
