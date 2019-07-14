<template>
  <div id="main">
    <div class="buttons">
      <app-button
        @click.native="rounds++">Add Round
      </app-button>
      <app-button
        @click.native="rounds--">Skip Round
      </app-button>
      <app-button
        @click.native="endRounds">End
      </app-button>
    </div>
    <div class="mode">
      <p v-if="workMode" class="work-mode">Work</p>
      <p v-else>Rest</p>
      <p id="timer">{{ minutes }}:{{ seconds }}</p>
    </div>
    <div class="details">
      <em>Work: {{ workTime }} mins</em> <br>
      <em>Rest: {{ restTime }} mins</em> <br>
      <em>Rounds: {{ rounds }}</em> <br>
      <em>Total time: {{(workTime + restTime) * rounds}} mins</em>
    </div>
  </div>
</template>

<script>
/* jshint esversion: 9 */
import { value, computed, onCreated } from 'vue-function-api';
import AppButton from './AppButton.vue';

export default {
name: 'Countdown',
setup() {
  const workMode = value(true);
  const workTime = value(25);
  const restTime = value(5);
  const rounds = value(5);
  const minutes = value();
  const seconds = value('00');

  const countdown = () => {
    const timeValue = setInterval(() => {
      if (seconds.value <= 10
          && seconds.value > 0) {
        seconds.value = '0' + String(seconds.value - 1);
      } else {
        seconds.value--;
      }
      if (seconds.value < 0) {
        seconds.value = 59;
        if (minutes.value === 0) {
          clearInterval(timeValue);
          endRounds();
          // console.log('End Rounds');
          return;
        } else {
          minutes.value--;
          seconds.value = 59;
        }
      }
    }, 300);
  };

  onCreated(() => {
    minutes.value = 10;
    countdown();
  });

  const endRounds = () => {
    minutes.value = 0;
    seconds.value = '00';
  };
  // const click = () => console.log('clicked');

  // TODO: Methods for countdown, skip round, end
    // countdown period -> (work -> rest) x rounds
    //    -> when rounds == 0, end

  return {
    workMode,
    workTime,
    restTime,
    rounds,
    seconds,
    minutes,
    endRounds,


    // click,
  };
},
components: {
  'app-button': AppButton,
},
};
</script>

<style scoped>

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
  top: 230px;
}

</style>
