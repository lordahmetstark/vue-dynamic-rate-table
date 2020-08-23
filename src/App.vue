<template>
  <div id="app">
    <img v-if="!isStart" src="./assets/stop.jpg" />
    <img v-else src="./assets/logo.png" />
    <div class="buttons">
      <button @click="reset()">Sıfırla</button>
      <button @click="start()">Başla</button>
    </div>
    <ScoreTable :isStart="isStart" />
  </div>
</template>

<script>
import ScoreTable from "./components/ScoreTable.vue";

export default {
  name: "App",
  components: {
    ScoreTable,
  },
  data() {
    return {
      isStart: false,
    };
  },
  methods: {
    reset: function () {
      let vm = this;

      vm.isStart = false;
    },
    start: function () {
      let vm = this;

      vm.isStart = true;
    },
  },
};
</script>

<style lang="scss">
@import "@/assets/main.scss";
</style>