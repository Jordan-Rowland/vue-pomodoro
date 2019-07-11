<template>
  <div id="main">
    <div class="buttons is-centered">
      <button class="button is-primary">Skip Round</button>
      <button class="end-btn button is-primary">End</button>
    </div>
    <p id="timer">3:30</p>
    <div class="details"><em>Rest: 5:00</em></div>
    <div class="details"><em>Rounds: 3</em></div>
    <div class="details"><em>Total time: 30:00</em></div>
  </div>
</template>

<script>
/* jshint esversion: 9 */
import { value } from 'vue-function-api';

export default {
name: 'Countdown',
setup() {
  const mode = value('work');


  return {
    mode,
  };
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

#timer {
  font-size: 4em;
  text-align: center;
  position: relative;
  top: 15px;
}

.buttons {
}

.button {
  /*position: relative;*/
}

.end-btn {
  /*margin-top: 8px;*/
  width: 105px;
}

.details {
  position: relative;
  top: 10px;
  font-size: 1.3em;
}
</style>
