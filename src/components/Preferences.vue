<template>
  <transition name="modal-fade">
    <div @click.self="close" class="backdrop">
      <div
        class="modal-container"
        role="dialog"
        aria-labelledby="Preferences"
        aria-describedby="Preferences"
      >
        <b-row>
          <b-col cols="12" class="d-flex align-items-center justify-content-between">
            <h4 class="mb-0">Preferences</h4>
            <b-icon class="clickable" icon="x" color="#6c757d" font-scale="2" @click="close">
            </b-icon>
          </b-col>
        </b-row>
        <form @submit.prevent="setPreferences" class="mt-3 mb-3">
          <div class="row">
            <b-form-group
              label="Pomodoro"
              label-for="pomodoro"
              class="col-6 mb-2"
            >
              <b-form-input id="pomodoro" v-model="preferences.focus" v-mask="'##:##'" />
            </b-form-group>
            <b-form-group
              label="Rounds"
              label-for="rounds"
              class="col-6 mb-2"
            >
              <b-form-input id="rounds" v-model="preferences.rounds" min="0" type="number" />
            </b-form-group>
            <b-form-group
              label="Short break"
              label-for="short-break"
              class="col-6 mb-2"
            >
              <b-form-input id="short-break" v-model="preferences.shortBreak" v-mask="'##:##'" />
            </b-form-group>
            <b-form-group
              label="Long break"
              label-for="long-break"
              class="col-6 mb-2"
            >
              <b-form-input id="long-break" v-model="preferences.longBreak" v-mask="'##:##'" />
            </b-form-group>
          </div>
        </form>
        <b-row>
          <b-col cols="12" class="d-flex align-items-center justify-content-end">
            <b-button variant="secondary" type="submit" class="text-white" @click="close">
              Cancel
            </b-button>
            <b-button variant="primary" type="submit" class="text-white">
              Save
            </b-button>
          </b-col>
        </b-row>
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
    border-radius: 12px;
    background-color: #fff;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    width: 35rem;
    padding: 20px;
    position: relative;
    -webkit-box-shadow: 0 3px 7px rgba(0, 0, 0, 0.3);
    -moz-box-shadow: 0 3px 7px rgba(0, 0, 0, 0.3);
    box-shadow: 0 3px 7px rgba(0, 0, 0, 0.3);
  }
}

.btn-secondary {
  margin-right: 15px;
}

.clickable {
  cursor: pointer;
}

@media screen and (max-width: 800px) {
  .modal-container  {
    width: 95vw;
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
