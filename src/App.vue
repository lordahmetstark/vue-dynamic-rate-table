<template>
  <div id="app">
    <git-hub />
    <logos :isStart="isStart" />
    <div class="buttons">
      <button @click="reset()">Sıfırla</button>
      <button @click="start()">Başla</button>
    </div>
    <score-table :isStart="isStart" />
  </div>
</template>

<script>
import ScoreTable from "./components/ScoreTable.vue";
import GitHub from "./components/GitHub.vue";
import Logos from "./components/Logos.vue";

export default {
  name: "App",
  components: {
    ScoreTable,
    GitHub,
    Logos,
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