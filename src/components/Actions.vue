<template>
<fragment>
  <b-row class="btns-container mt-4">
    <b-col cols="4" class="d-flex justify-content-center">
      <button class="btn btn-outline border-opacity" @click="toggleModal">
        <b-icon icon="gear-fill" color="#fff" scale="1.1"></b-icon>
      </button>
    </b-col>
    <b-col cols="4" class="d-flex justify-content-center">
      <button class="btn btn-outline" @click="toggleIsPlaying">
        <b-icon v-if="isPlaying" icon="pause-fill" color="#fff" scale="1.3"></b-icon>
        <b-icon v-else icon="play-fill" color="#fff" scale="1.3"></b-icon>
      </button>
    </b-col>
    <b-col cols="4" class="d-flex justify-content-center">
      <button class="btn btn-outline border-opacity" @click="skipStep">
        <b-icon icon="skip-end-fill" color="#fff" scale="1.2"></b-icon>
      </button>
    </b-col>
  </b-row>
  <Preferences
    v-show="isShowingPreferences"
    @setPreferences="setPreferences"
    @close="toggleModal"
  />
</fragment>
</template>

<script>
export default {
  components: {
    Preferences: () => import('@/components/Preferences.vue'),
  },
  data() {
    return {
      isPlaying: false,
      isShowingPreferences: false,
    };
  },
  methods: {
    setPreferences(preferences) {
      this.$emit('setPreferences', preferences);
    },
    skipStep() {
      this.$emit('skipStep');
    },
    toggleIsPlaying() {
      this.isPlaying = !this.isPlaying;
      this.$emit('toggleIsPlaying', this.isPlaying);
    },
    toggleModal() {
      this.isShowingPreferences = !this.isShowingPreferences;
    },
  },
};
</script>

<style lang="scss" scoped>
.btns-container {
  width: 55%;
  margin: 0 auto;
  .btn-outline {
    height: 50px;
    width: 50px;
    border: 2px solid #fff;
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    &:focus {
      outline: 0;
      box-shadow: none;
    }
    &.border-opacity {
      border: 2px solid rgba(255, 255, 255, 0.4);
    }
  }
}

@media screen and (max-width: 800px) {
  .btns-container {
    width: 100%;
  }
}
</style>
