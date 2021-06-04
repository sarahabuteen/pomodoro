<template functional>
  <b-navbar class="p-3" toggleable variant="faded" type="light">
    <b-navbar-brand class="text-white">Pomodoro Timer</b-navbar-brand>
    <b-navbar-nav class="mr-auto">
      <b-nav-item href="https://en.wikipedia.org/wiki/Pomodoro_Technique" target="_blank">
        <b-icon icon="exclamation-circle-fill" color="#fff" scale="1.4"></b-icon>
      </b-nav-item>
    </b-navbar-nav>
  </b-navbar>
</template>

<style lang="scss" scoped>
  @import url('https://fonts.googleapis.com/css2?family=Pacifico&display=swap');

  .navbar-brand {
    font-size: 1.7rem;
    font-weight: 500;
    font-family: 'Pacifico', cursive;
  }
</style>
