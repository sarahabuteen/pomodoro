<template>
  <div :class="`${wrapperClassName}`">
    <b-container fluid>
      <b-row>
        <b-col cols="12">
          <Header />
        </b-col>
      </b-row>
    </b-container>
    <b-container class="d-flex flex-column justify-content-center align-items-center">
      <b-row>
        <b-col cols="12" class="d-flex justify-content-center flex-column align-items-center">
          <Timer
            :timer="actualStep.time"
            :isPlaying="isPlaying"
            @timeFinished="setNextStep"
          />
          <h2 class="mt-4 text-white">{{ actualStep.title }}</h2>
          <h4 class="text-white mb-0">{{ actualRound }}/{{ rounds }} rounds</h4>
        </b-col>
      </b-row>
      <actions
        @setPreferences="setPreferences"
        @toggleIsPlaying="setIsPlaying"
        @skipStep="setNextStep"
      />
    </b-container>
    <Footer />
  </div>
</template>

<script>
import Header from '@/components/Header.vue';
import Footer from '@/components/Footer.vue';
import Timer from '@/components/Timer.vue';
import Actions from '@/components/Actions.vue';
import timer from '@/enums/timer';

const {
  focus,
  shortBreak,
  longBreak,
  rounds,
} = timer;

export default {
  name: 'Pomodoro',
  components: {
    Header,
    Timer,
    Actions,
    Footer,
  },
  data() {
    return {
      actualRound: 1,
      rounds,
      isPlaying: false,
      actualStep: null,
      steps: {
        focus: {
          time: focus.time,
          title: focus.label,
        },
        shortBreak: {
          time: shortBreak.time,
          title: shortBreak.label,
        },
        longBreak: {
          time: longBreak.time,
          title: longBreak.label,
        },
      },
    };
  },
  created() {
    this.setActualStep(this.steps.focus);
  },
  computed: {
    wrapperClassName() {
      if (!this.actualStep) return '';
      const step = {
        [focus.label]: 'focus',
        [shortBreak.label]: 'short',
        [longBreak.label]: 'long',
      };
      return `${step[this.actualStep.title]}-wrapper`;
    },
  },
  methods: {
    setNextStep() {
      const { title } = this.actualStep;
      if (title === longBreak.label) {
        this.setActualRound(1);
        this.setActualStep(this.steps.focus);
      } else if (title === focus.label && this.actualRound === this.rounds) {
        this.setActualStep(this.steps.longBreak);
      } else if (title === focus.label && this.actualRound !== this.rounds) {
        this.setActualStep(this.steps.shortBreak);
      } else if (title === shortBreak.label && this.actualRound !== this.rounds) {
        this.setActualStep(this.steps.focus);
        this.setActualRound(this.actualRound + 1);
      }
    },
    setIsPlaying(value) {
      this.isPlaying = value;
    },
    setActualStep(step) {
      this.actualStep = step;
    },
    setActualRound(value) {
      this.actualRound = value;
    },
    setPreferences(steps) {
      Object.entries(steps).forEach(([key, value]) => {
        if (key === 'rounds') {
          this.rounds = +value;
        } else {
          this.steps[key].time = value;
        }
        this.setActualRound(1);
        this.setActualStep(this.steps.focus);
      });
    },
  },
};
</script>

<style lang="scss" scoped>
.wrapper,
.focus-wrapper,
.short-wrapper,
.long-wrapper {
  display: grid;
  grid-template-rows: 1rem 1fr;
  height: 100vh;
}
.focus-wrapper {
  background: #DB524D;
}
.short-wrapper {
  background: #468D91;
}
.long-wrapper {
  background: #417FA7;
}
.content {
  display: grid;
  grid-row-gap: 2rem;
  grid-template-rows: 4rem 50% 3rem 6rem;
  justify-items: center;
  align-items: center;
}
@media screen and (max-width: 800px) {
  .content {
    grid-row-gap: 0.5rem;
    grid-template-rows: 12% 50% 15% 20%;
  }
}
.step-title {
  font-size: 2.1rem;
  font-weight: 400;
}
@media screen and (max-width: 800px) {
  .step-title {
    font-size: 1.7rem;
  }
}
.rounds {
  letter-spacing: 0.1rem;
}
</style>
