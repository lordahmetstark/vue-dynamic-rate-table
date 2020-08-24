<template>
  <img v-if="!isStart" src="../assets/stop.jpg" />
  <img v-else src="../assets/logo.png" />
</template>

<script>
export default {
  props: {
    isStart: {
      type: Boolean,
      default: false,
    },
  },
};
</script>