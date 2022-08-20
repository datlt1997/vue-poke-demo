<template>
  <MainScreen
    v-if="statusMatch === 'default'"
    @onStart="onHandleBeforeStart($event)"
  />
  <InteractScreen
    v-if="statusMatch === 'match'"
    :cardsContext="setting.cardsContext"
    @onFinish="onGetResult"
  />
  <ResultScreen
    v-if="statusMatch === 'result'"
    :timer="timer"
    @onStart="statusMatch = 'default'"
  />
  <p class="copyright">
    This game demo by Datlt in Ytb in Vue 3 -
    <a
      href="https://www.youtube.com/watch?v=CHM75-NqOmk&list=PLU4OBh9yHE94sZ3TPGt0QG_PIwrZ1QF6i"
      >view here</a
    >
  </p>
</template>

<script>
import MainScreen from "./components/MainScreen.vue";
import InteractScreen from "./components/InteractScreen.vue";
import ResultScreen from "@/components/ResultScreen";

import { shuffled } from "./utils/array";
export default {
  components: {
    MainScreen,
    InteractScreen,
    ResultScreen,
  },
  name: "App",
  data() {
    return {
      setting: {
        totalOfBlocks: 0,
        cardsContext: [],
        startedAt: null,
      },
      statusMatch: "default",
      timer: 0,
    };
  },

  methods: {
    onHandleBeforeStart(config) {
      console.log("running game with config", event);
      this.setting.totalOfBlocks = config.totalOfBlocks;

      const firstCards = Array.from(
        { length: this.setting.totalOfBlocks / 2 },
        (_, i) => i + 1
      );
      const secondCards = [...firstCards];
      const cards = [...firstCards, ...secondCards];
      console.log(cards);

      this.setting.cardsContext = shuffled(shuffled(shuffled(shuffled(cards))));
      this.setting.startedAt = new Date().getTime();
      this.statusMatch = "match";
    },
    onGetResult() {
      //get Timer
      this.timer = new Date().getTime() - this.setting.startedAt;

      //switch screen
      this.statusMatch = "result";
    },
  },
};
</script>
<style scoped>
.copyright {
  position: fixed;
  left: 50%;
  transform: translateX(-50%);
  bottom: 1.5rem;
  color: var(--light);
  z-index: 3;
  font-size: 1.5rem;
}
.copyright a {
  color: #f4dc26;
}
</style>
