<template>
  <b-container fluid>
    <b-row>
      <b-col cols="12">
      <p class="text-white text-center">
        Hand-crafted & made with <b-icon icon="suit-heart-fill"></b-icon> by
        <span class="text-underline clickable" @click="openLinkedin">Sarah Abuteen</span>
      </p>
      </b-col>
    </b-row>
  </b-container>
</template>

<script>
export default {
  methods: {
    openLinkedin() {
      window.open('https://www.linkedin.com/in/sarahabuteen/', '_blank');
    },
  },
};
</script>

<style lang="scss" scoped>
  .text-underline {
    text-decoration: underline;
  }
  .clickable {
    cursor: pointer;
  }
</style>
