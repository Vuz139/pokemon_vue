<template>
  <main-screen
    v-if="statusMatch === 'default'"
    @onStart="onHandleBeforeStart($event)"
  />
  <interact-screen
    v-if="statusMatch === 'match'"
    :cardsContext="settings.cardsContext"
    @onFinish="onGetResult"
  />
  <result-screen
    v-if="statusMatch === 'result'"
    :timer="timer"
    @onStartAgain="handleStartAgain"
  />
  <copy-right-screen-vue />
</template>
<script>
import InteractScreen from "./components/InteractScreen.vue";
import MainScreen from "./components/MainScreen.vue";
import { shuffled } from "./utils/array";
import ResultScreen from "./components/ResultScreen.vue";
import CopyRightScreenVue from "./components/CopyRightScreen.vue";
export default {
  name: "App",
  data() {
    return {
      statusMatch: "default",
      settings: {
        totalOfBlocks: 0,
        cardsContext: [],
        startedAt: null,
      },
      timer: 0,
    };
  },

  components: {
    MainScreen,
    InteractScreen,
    ResultScreen,
    CopyRightScreenVue,
  },
  methods: {
    onHandleBeforeStart(config) {
      this.settings.totalOfBlocks = config.totalOfBlocks;
      const firstCards = Array.from(
        {
          length: this.settings.totalOfBlocks / 2,
        },
        (_, i) => i + 1
      );
      const secondCards = [...firstCards];
      const cards = [...firstCards, ...secondCards];
      this.settings.cardsContext = shuffled(shuffled(cards));
      this.settings.startedAt = new Date().getTime();
      // data ready
      this.statusMatch = "match";
    },
    onGetResult() {
      const getTimer = new Date().getTime();
      this.timer = getTimer - this.settings.startedAt;
      this.statusMatch = "result";
    },
    handleStartAgain() {
      this.statusMatch = "default";
    },
  },
};
</script>
