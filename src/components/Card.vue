<template>
  <div
    @click="onToggleFlipCard"
    class="card"
    :class="{ 'is-disabled': isDisable }"
  >
    <div class="card__inner" :class="{ 'is-flipped': isFlipped }">
      <div class="card__face card__face--front">
        <div class="card__content"></div>
      </div>
      <div class="card__face card__face--back">
        <div
          class="card__content"
          :style="{
            backgroundImage: `url(${require('@/assets/' + imgBackFaceUrl)})`,
          }"
        ></div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    imgBackFaceUrl: {
      type: String,
      required: true,
    },
    card: {
      type: [String, Number, Array, Object],
      required: true,
    },
  },
  setup() {},
  data() {
    return {
      isFlipped: false,
      isDisable: false,
    };
  },
  methods: {
    onToggleFlipCard() {
      if (this.isDisable) return;
      this.isFlipped = !this.isFlipped;
      if (this.isFlipped) this.$emit("onFlip", this.card);
    },
    onFlipBackCard() {
      this.isFlipped = false;
    },
    onDisable() {
      this.isDisable = true;
    },
  },
  name: "CardComponent",
};
</script>

<style lang="css" scoped>
.card.is-disabled {
  cursor: default;
}
.card {
  display: inline-block;
  margin-right: 1rem;
  margin-bottom: 1rem;
  width: 90px;
  height: 120px;
}

.card__inner {
  width: 100%;
  height: 100%;
  transition: transform 1s;
  transform-style: preserve-3d;
  cursor: pointer;
  position: relative;
}
.card__inner.is-flipped {
  transform: rotateY(-180deg);
}
.card__face {
  position: absolute;
  width: 100%;
  height: 100%;
  backface-visibility: hidden;
  overflow: hidden;
  border-radius: 1rem;
  padding: 1rem;
  box-shadow: 0px 3px 10px rgba(0, 0, 0, 0.2);
}
.card__face--front .card__content {
  background: url("../assets/images/icon_back.png") no-repeat center center;
  background-size: 35px 55px;
}
.card__content {
  background: no-repeat center center;
  background-size: 100% 100%;
  height: 100%;
  width: 100%;
}
.card__face--back {
  background-color: var(--light);
  transform: rotateY(-180deg);
}
</style>
