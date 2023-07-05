<template>
  <div class="screen">
    <div class="screen__inner">
      <card-flip
        v-for="(card, index) in cardsContext"
        :key="index"
        :imgBackFaceUrl="`images/${card}.png`"
        :card="{ card, index }"
        :ref="`card-${index}`"
        @onFlip="checkRule($event)"
      />
    </div>
  </div>
</template>
<script>
import CardFlip from "./Card.vue";
export default {
  props: {
    cardsContext: {
      type: Array,
      default: () => [],
    },
  },
  setup() {},
  components: {
    CardFlip,
  },
  data() {
    return {
      rules: [],
    };
  },
  methods: {
    checkRule(card) {
      if (this.rules.length === 2) return false;

      this.rules.push(card);

      if (this.rules.length === 2) {
        if (this.rules[0].card === this.rules[1].card) {
          this.$refs[`card-${this.rules[0].index}`][0].onDisable();
          this.$refs[`card-${this.rules[1].index}`][0].onDisable();
          this.rules = [];
          const disableElements = document.querySelectorAll(
            ".screen .card.is-disabled"
          );

          if (disableElements.length === this.cardsContext.length - 2) {
            setTimeout(() => {
              this.$emit("onFinish");
            }, 920);
          }
        } else {
          setTimeout(() => {
            this.$refs[`card-${this.rules[0].index}`][0].onFlipBackCard();
            this.$refs[`card-${this.rules[1].index}`][0].onFlipBackCard();
            this.rules = [];
          }, 800);
        }
      } else {
        return false;
      }
    },
  },
};
</script>

<style lang="css" scoped>
.screen {
  width: 100%;
  height: 100vh;
  overflow-y: scroll;
  position: absolute;
  top: 0;
  left: 0;
  z-index: 2;
  background-color: var(--dark);
  color: var(--light);
}
.screen__inner {
  width: 424px;
  display: flex;

  flex-wrap: wrap;
  margin: 2rem auto;
}
</style>
