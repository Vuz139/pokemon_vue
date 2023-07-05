<template>
  <div class="screen">
    <h1>Congratulations</h1>
    <p>{{ Math.round(timer / 1000, 2) }} seconds</p>
    <button @click="onStartAgain">Start Again</button>
  </div>
</template>

<script>
export default {
  setup() {},
  props: {
    timer: {
      type: Number,
      required: true,
    },
  },
  methods: {
    onStartAgain() {
      this.$emit("onStartAgain");
    },
  },
};
</script>

<style lang="css" scoped>
.screen {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  font-size: 1.6rem;
  flex-direction: column;
  background-color: var(--dark);
  color: var(--light);
}
h1 {
  font-size: 5rem;
}
p {
  font-size: 2.6rem;
}
button {
  font-family: var(--font);
  margin-top: 1rem;
  padding: 1rem 2rem;
  font-size: 2rem;
  border: none;
  border-radius: 0.5rem;
  transition: all 0.5s linear;
}
button:hover {
  cursor: pointer;
  scale: 1.1;
}
</style>
