<template>
  <div class="screen">
    <h1>✨ Congratulations ✨</h1>
    <h3>{{ Math.round(timer / 1000) }} seconds</h3>
    <button @click="onStartAgain">Start Again</button>
  </div>
</template>
<script>
export default {
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
  width: 100%;
  min-height: 100dvh;
  padding: 1rem;
  position: absolute;
  top: 0;
  left: 0;
  z-index: 2;
  background-color: var(--dark);
  color: var(--light);
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
}

.screen h1 {
  font-size: clamp(2.5rem, 12vw, 5rem);
  text-align: center;
}

.screen h3 {
  margin-top: 1.5rem;
  font-size: clamp(2rem, 8vw, 3rem);
}

.screen button {
  font: var(--font);
  background: transparent;
  box-shadow: none;
  border: 1px solid var(--light);
  color: var(--light);
  margin: 1rem;
  padding: 1rem 1.25rem;
  border-radius: 0.5rem;
  font-size: 1.25rem;
  cursor: pointer;
  transition: background 0.3s ease-in-out;
}

.screen button:hover {
  background-color: var(--light);
  color: var(--dark);
}
</style>
