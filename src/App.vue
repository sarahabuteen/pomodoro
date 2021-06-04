<template>
  <div id="app">
    <pomodoro />
  </div>
</template>

<script>
import Pomodoro from '@/components/Pomodoro.vue';

export default {
  name: 'App',
  components: {
    Pomodoro,
  },
};
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
}
</style>
