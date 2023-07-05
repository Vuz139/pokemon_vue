<template>
  <div class="screen">
    <div class="screen__inner">
      <h1>POKE MEMORIES</h1>
      <h3>Select mode to start game</h3>
      <div class="actions">
        <button @click="onStart(4)">
          <p class="actions__num">4x4</p>
          <span class="actions__level">Easy</span>
        </button>
        <button @click="onStart(6)">
          <p class="actions__num">6x6</p>
          <span class="actions__level">Normal</span>
        </button>
        <button @click="onStart(8)">
          <p class="actions__num">8x8</p>
          <span class="actions__level">Hard</span>
        </button>
        <button @click="onStart(10)">
          <p class="actions__num">10x10</p>
          <span class="actions__level">Super Hard</span>
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  setup() {},
  methods: {
    onStart(n) {
      this.$emit("onStart", { totalOfBlocks: n * n });
    },
  },
};
</script>

<style scoped>
.screen {
  background-color: var(--dark);
  color: var(--light);
  height: 100vh;
  display: flex;
}
.screen__inner {
  margin: auto;
}
h1 {
  font-size: 5rem;
  text-align: center;
}
h3 {
  text-align: center;
  font-size: 2rem;
  font-weight: 200;
}
.actions {
  margin-top: 1rem;
  display: flex;
  gap: 1rem;
}
button {
  width: 130px;
  height: 130px;
  border: 1px solid var(--light);
  color: var(--light);
  background-color: var(--dark);
  border-radius: 0.6rem;
  font-family: var(--font);
  transition: all 0.3s linear;
}
.actions__num {
  font-size: 2.2rem;
}
.actions__level {
  font-size: 1.6rem;
}
button:hover {
  background-color: var(--light);
  cursor: pointer;
  color: var(--dark);
}
</style>
