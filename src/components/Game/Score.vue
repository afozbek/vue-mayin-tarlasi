<template>
  <div class="modal">
    <div>Score: {{score}}</div>
    <button @click="handleFailed">Try Again</button>
    <button @click="handleFailed">New Game</button>
  </div>
</template>

<script>
export default {
  name: "Score",
  props: ["score"],
  methods: {
    handleFailed() {
      this.$emit("handleFailed");
    }
  }
};
</script>

<style>
.modal {
}
</style>