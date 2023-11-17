<template>
  <main-screen
    v-if="statusMatch === 'default'"
    @onStart="onHandleBeforeStart($event)"
  >
  </main-screen>
  <interact-screen
    v-if="statusMatch === 'match'"
    :cardsContext="settings.cardsContext"
    @onFinish="onGetResult"
  ></interact-screen>
  <result-screen
    :timer="timer"
    v-if="statusMatch === 'result'"
    @onStartAgain="statusMatch = 'default'"
  ></result-screen>
  <copy-right></copy-right>
</template>

<script>
import MainScreen from "./components/MainScreen.vue";
import InteractScreen from "./components/InteractScreen.vue";
import CopyRight from "./components/CopyRight.vue";
import ResultScreen from "./components/ResultScreen.vue";

import { shuffled } from "./ultis/array";
export default {
  name: "App",
  components: {
    MainScreen,
    InteractScreen,
    CopyRight,
    ResultScreen,
  },
  data() {
    return {
      settings: {
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
      console.log("Running handle before start, ", config);
      this.settings.totalOfBlocks = config.totalOfBlocks;
      const firstCards = Array.from(
        { length: this.settings.totalOfBlocks / 2 },
        (_, i) => i + 1
      );
      const secondCards = [...firstCards];
      const cards = [...firstCards, ...secondCards];
      console.log(cards);
      this.settings.cardsContext = shuffled(
        shuffled(shuffled(shuffled(cards)))
      );
      this.settings.startedAt = new Date().getTime();
      console.log(this.settings.startedAt);
      //data ready
      this.statusMatch = "match";
    },
    onGetResult() {
      //get timer
      this.timer = new Date().getTime() - this.settings.startedAt;
      //switch to result component
      this.statusMatch = "result";
    },
  },
};
</script>
