<template>
  <MainScreen
    v-if="statusMatch === 'default'"
    @onStart="onHandleBeforeStart($event)"
  />
  <InteractScreen
    v-if="statusMatch === 'match'"
    :cardsContext="setting.cardsContext"
  />
</template>

<script>
import MainScreen from "./components/MainScreen.vue";
import InteractScreen from "./components/InteractScreen.vue";

import { shuffled } from "./utils/array";
export default {
  name: "App",
  data() {
    return {
      setting: {
        totalOfBlocks: 0,
        cardsContext: [],
        startedAt: null,
      },
      statusMatch: "default",
    };
  },
  components: {
    MainScreen,
    InteractScreen,
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
  },
};
</script>
