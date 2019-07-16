<template>
  <div id="main">
    Work duration(minutes):
     <br> <input type="text" name=""> <br>
    Rest duration(minutes):
     <br> <input type="text" name=""> <br>
    Rounds:
     <br> <input type="number" name="" value="3">
     <app-button id="start-button">
       Start!
     </app-button>
  </div>
</template>

<script>
/* jshint esversion: 9 */
import { value } from 'vue-function-api';
import AppButton from './AppButton.vue';

export default {
name: 'PSetup',
setup() {
  const startCountdown = () => {

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
