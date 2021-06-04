<template>
  <transition name="modal-fade">
    <div @click.self="close" class="backdrop">
      <div
        class="modal-container"
        role="dialog"
        aria-labelledby="Preferences"
        aria-describedby="Preferences"
      >
        <header>
          <h4 class="mb-0">Preferences</h4>
          <b-button class="close-btn" variant="danger" @click="close">
            <b-icon icon="x" color="#fff" font-scale="1.4"></b-icon>
          </b-button>
        </header>
        <main class="content">
          <form @submit.prevent="setPreferences">
            <div class="form-content">
              <b-form-group
                label="Pomodoro"
                label-for="pomodoro"
              >
                <b-form-input id="pomodoro" v-model="preferences.focus" v-mask="'##:##'" />
              </b-form-group>
              <b-form-group
                label="Rounds"
                label-for="rounds"
              >
                <b-form-input id="rounds" v-model="preferences.rounds" min="0" type="number" />
              </b-form-group>
              <b-form-group
                label="Short break"
                label-for="short-break"
              >
                <b-form-input id="short-break" v-model="preferences.shortBreak" v-mask="'##:##'" />
              </b-form-group>
              <b-form-group
                label="Long break"
                label-for="long-break"
              >
                <b-form-input id="long-break" v-model="preferences.longBreak" v-mask="'##:##'" />
              </b-form-group>
            </div>
            <div class="d-flex justify-content-end">
              <b-button variant="primary" type="submit" class="text-white">
                Submit
              </b-button>
            </div>
          </form>
        </main>
      </div>
    </div>
  </transition>
</template>

<script>
import { mask } from 'vue-the-mask';
import timer from '@/enums/timer';

const {
  focus,
  shortBreak,
  longBreak,
  rounds,
} = timer;

export default {
  directives: { mask },
  data() {
    return {
      preferences: {
        focus: focus.time,
        shortBreak: shortBreak.time,
        longBreak: longBreak.time,
        rounds,
      },
    };
  },
  methods: {
    close() {
      this.$emit('close');
    },
    setPreferences() {
      this.$emit('setPreferences', this.preferences);
      this.close();
    },
  },
};
</script>

<style lang="scss" scoped>
.backdrop {
  position: fixed;
  z-index: 100;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  background-color: rgba(0,0,0,0.5);
  display: flex;
  justify-content: center;
  align-items: center;
  .modal-container {
    border-radius: 5px;
    background-color: #fff;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    width: 35rem;
    padding: 20px;
    position: relative;
    header {
      display: flex;
      align-items: center;
      justify-content: space-between;
      .close-btn {
        border-radius: 50%;
        height: 28px;
        width: 28px;
        display: flex;
        align-items: center;
        justify-content: center;
      }
    }
    .content {
      .form-content {
        display: grid;
        justify-content: space-around;
        grid-template-rows: repeat(2, 1fr);
        grid-template-columns: repeat(2, 44%);
        row-gap: 2rem;
        column-gap: 4rem;
        margin: 1rem 0;
      }
    }
  }
}

@media screen and (max-width: 800px) {
  .modal-container  {
    width: 95vw;
  }
}

@media screen and (max-width: 800px) {
  .form-content {
    grid-template-columns: 90%;
    grid-template-rows: 10%;
    margin: 2rem 0;
  }
}

.modal-fade-enter,
.modal-fade-leave-active {
  opacity: 0;
  top: -10px;
}
.modal-fade-enter-active,
.modal-fade-leave-active {
  transition: all 0.4s ease;
}
</style>
