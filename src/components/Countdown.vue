<template>
  <div id="main">
    <div class="buttons">
      <app-button
        @click.native="addRound">Add Round
      </app-button>
      <app-button
        @click.native="skipRound">Skip Round
      </app-button>
      <app-button
        @click.native="endRounds">End
      </app-button>
    </div>
    <div class="mode">
      <transition name="flip" mode="out-in">
        <p key=1 v-if="workMode" class="work-mode">Work</p>
        <p key=2 v-else class="work-mode">Rest</p>
      </transition>
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
import { computed, value, onCreated, watch } from 'vue-function-api';
import AppButton from './AppButton.vue';

export default {
name: 'Countdown',

props: {
  workTimeProp: Number,
  restTimeProp: Number,
  roundsProp: Number,
},

setup(props, context) {
  const workMode = value(true);
  const countdownRunning = value(true);
  const workTime = computed(() => props.workTimeProp);
  const restTime = computed(() => props.restTimeProp);
  const rounds = value(props.roundsProp);
  const roundsLeft = value();
  const minutes = value();
  const seconds = value('00');

  const countdown = () => {
    const timeValue = setInterval(() => {
      if (!countdownRunning.value) {
        console.log(countdownRunning.value)
        clearInterval(timeValue);
        endRounds();
      }
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
            endRounds();
          } else {
            if (!workMode.value) {
              minutes.value = workTime.value - 1;
              roundsLeft.value--;
            } else {
              minutes.value = restTime.value - 1;
            }
            changeMode();
          }
        } else {
          minutes.value--;
          seconds.value = 59;
        }
      }
    }, 50);
  };

  const addRound = () => {
    roundsLeft.value++;
    rounds.value++;
  };

  const skipRound = () => {
    if (roundsLeft.value < 1) {
      roundsLeft.value = 0;
    } else {
      roundsLeft.value--;
    }
    workMode.value = true;
    seconds.value = '00';
    minutes.value = props.workTimeProp;
  };

  const endRounds = () => {
    countdownRunning.value = false;
    roundsLeft.value = 0;
    minutes.value = 0;
    seconds.value = '00';
    let endTone = play('endTone');
    endTone.play();
    context.emit('emitEndRounds');
  };

  const play = (sound) => {
    const audio = new Audio(require(`../assets/${sound}.mp3`));
    return audio
  };

  const changeMode = () => {
    workMode.value = !workMode.value;
    if (workMode.value) {
      let ding1 = play('ding1');
      ding1.play();
    } else {
      let ding2 = play('ding2');
      ding2.play();
    }
    return [ding1, ding2]
  };

  onCreated(() => {
    countdownRunning.value = true;
    roundsLeft.value = rounds.value;
    minutes.value = workTime.value;
    countdown();
    let ding1 = play('ding1');
    ding1.play();
  });

  return {
    workMode,
    workTime,
    restTime,
    rounds,
    roundsLeft,
    minutes,
    seconds,
    addRound,
    skipRound,
    endRounds,
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

/* Animation 'flip' */
.flip-enter {
  opacity: 1;
  /*transform: rotateY(90deg);*/
  transform: scale(1.5);
}
.flip-enter-active {
  transition: all .6s cubic-bezier(0.55, 0.085, 0.68, 0.53);
}
.flip-leave {
  transform: scaleX(0) translateZ(0);
  opacity: 0;
}
.flip-leave-active {
  transition: all .35s cubic-bezier(0.25, 0.46, 0.45, 0.94);
}

</style>
