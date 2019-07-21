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
import { computed,
         value,
         onCreated,
         onDestroyed } from 'vue-function-api';
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
  const workTime = computed(() => props.workTimeProp);
  const restTime = computed(() => props.restTimeProp);
  const rounds = value(props.roundsProp);
  const roundsLeft = value();
  const minutes = value();
  const seconds = value('00');
  let timeValue = value();

  const play = (sound) => {
  const audio = new Audio(require(`../assets/${sound}.mp3`));
  return audio;
  };

  const endTone = play('endTone');
  const ding1 = play('ding1');
  const ding2 = play('ding2');

  const formatSeconds = () => {
    if (seconds.value <= 10
        && seconds.value > 0) {
      seconds.value = `0${seconds.value - 1}`;
    } else {
      seconds.value--;
    }
  };

  const changeModes = () => {
    if (workMode.value) {
      minutes.value = restTime.value - 1;
    } else {
      minutes.value = workTime.value - 1;
      roundsLeft.value--;
    }
    changeMode();
  };

  const endAllRounds = () => {
    clearInterval(timeValue);
    endRounds();
    endTone.play();
  };

  const minusMinute = () => {
    minutes.value--;
    seconds.value = 59;
  };


  const countdown = () => {
    const endOrMinusMinute = (condition) => {
      if (condition) {
        endOrChangeModes(roundsAreOne);
      } else {
        minusMinute();
      }
    };

    const endOrChangeModes = (condition) => {
      if (condition && !workMode.value) {
        endAllRounds();
      } else {
        changeModes();
      }
    };

    timeValue = setInterval(() => {
      const secondsAreZero = seconds.value == 0;
      const minutesAreZero = minutes.value === 0;
      const roundsAreOne = roundsLeft.value === 1;

      formatSeconds();

      if (secondsAreZero) {
        seconds.value = 59;

        endOrMinusMinute(minutesAreZero);

      }
    }, 50);
  };

  const addRound = () => {
    roundsLeft.value++;
    rounds.value++;
  };

  const skipRound = () => {
    if (roundsLeft.value < 2) {
      endRounds();
    } else {
      roundsLeft.value--;
      ding1.play();
    }
    workMode.value = true;
    seconds.value = '00';
    minutes.value = props.workTimeProp;
  };

  const endRounds = () => {
    roundsLeft.value = 0;
    minutes.value = 0;
    seconds.value = '00';
    context.emit('emitEndRounds');
    endTone.play();
  };

  const changeMode = () => {
    workMode.value = !workMode.value;
    if (workMode.value) {
      ding1.play();
    } else {
      ding2.play();
    }
  };

  onCreated(() => {
    roundsLeft.value = rounds.value;
    minutes.value = workTime.value;
    countdown();
    ding1.play();
  });

  onDestroyed(() => {
    // console.log('unDestroyed');
    clearInterval(timeValue);
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
