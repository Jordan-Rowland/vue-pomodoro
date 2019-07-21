<template>
  <div id="main">
    Work duration(minutes): <input type="number" v-model="info.work"> <br>
    Rest duration(minutes): <input type="number" v-model="info.rest"> <br>
    Rounds: <input type="number" v-model="info.rounds">
     <app-button
      @click.native="startCountdown"
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

props: {
  workTimeProp: Number,
  restTimeProp: Number,
  roundsProp: Number,
},

setup(props, context) {

  const info = state({
    work: props.workTimeProp || 25,
    rest: props.restTimeProp || 5,
    rounds: props.roundsProp || 3,
  });

  const startCountdown = () => {
    context.emit('emitUp', info);
  };

  return {
    info,
    startCountdown,
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
  font-size: 1.2rem;
}

#start-button {
  margin-top: 1rem;
}

input {
  border: none;
  border-bottom: .1rem #5FBA7D solid;
  width: 35px;
  margin-left: 20px;
  font-size: 1.2rem;
}
</style>
