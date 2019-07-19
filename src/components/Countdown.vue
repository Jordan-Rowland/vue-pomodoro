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
      <p v-else class="work-mode">Rest</p>
      <p id="timer">{{ minutes }}:{{ seconds }}</p>
    </div>
    <div class="details">
      <em>Work: {{ workTime }} mins</em> <br>
      <em>Rest: {{ restTime }} mins</em> <br>
      <em>Rounds left: {{ roundsLeft }}</em> <br>
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

props: {
  workTimeProp: Number,
  restTimeProp: Number,
  roundsProp: Number,
},

setup(props) {
  const workMode = value(true);
  // const workTime = value(4);
  // const restTime = value(2);
  // const rounds = value(2);
  const workTime = computed(() => props.workTimeProp);
  const restTime = computed(() => props.restTimeProp);
  const rounds = computed(() => props.roundsProp);
  const roundsLeft = value();
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
          if (roundsLeft.value === 1 && !workMode.value) {
            clearInterval(timeValue);
            roundsLeft.value = 0;
            seconds.value = '00';
          } else {
            if (!workMode.value) {
              minutes.value = workTime.value - 1;
              roundsLeft.value--;
            } else {
              minutes.value = restTime.value - 1;
            }
            workMode.value = !workMode.value;
          }
        } else {
          minutes.value--;
          seconds.value = 59;
        }
      }
      // Change time back to 1000
    }, 10);
  };

  const endRounds = () => {
    // end button will send up event to change component
    // to PSetup component
    roundsLeft.value = 0;
    minutes.value = 0;
    seconds.value = '00';
  };

  onCreated(() => {
    roundsLeft.value = rounds.value;
    minutes.value = workTime.value;
    countdown();
  });

  return {
    workMode,
    workTime,
    restTime,
    rounds,
    roundsLeft,
    minutes,
    seconds,
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
