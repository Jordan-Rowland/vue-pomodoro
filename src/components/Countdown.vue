<template>
  <div id="main">
    <div class="buttons">
      <button
        @click="rounds++"
        class="button">Add Round</button>
      <button
        @click="rounds--"
        class="button">Skip Round</button>
      <button
        @click=""
        class="button">End</button>
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

export default {
name: 'Countdown',
setup() {
  const workMode = value(true);
  const workTime = value(25);
  const restTime = value(5);
  const rounds = value(5);

  return {
    workMode,
    workTime,
    restTime,
    rounds,
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

.button {
  margin: 0 15px;
  height: 3em;
  background-color: #5FBA7D;
  color: white;
  border: none;
  border-radius: 7px;
  width: 105px;
  font-weight: 800;
  box-shadow: none;
  outline: none;
}

.button:hover {
  cursor: pointer;
}

.details {
  position: absolute;
  font-size: 1.3em;
  top: 250px;
}
</style>
