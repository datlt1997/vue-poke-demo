<template>
  <div class="screen">
    <h1>POKE MEMORIES</h1>
    <h3>Select mode to start game</h3>
    <div class="actions">
      <button @click="onStart(16)">
        <span>4 X 4</span>
        <span>Easy</span>
      </button>

      <button @click="onStart(36)">
        <span>6 X 6</span>
        <span>Nomals</span>
      </button>
      <button @click="onStart(64)">
        <span>8 X 8</span>
        <span>Hard</span>
      </button>
      <button @click="onStart(100)">
        <span>10 X 10</span>
        <span>Super Hard</span>
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: "MainScreen",
  methods: {
    onStart(totalOfBlocks) {
      this.$emit("onStart", { totalOfBlocks });
    },
  },
};
</script>

<style></style>
