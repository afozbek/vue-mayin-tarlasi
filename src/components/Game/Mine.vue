<template>
  <div>
    <div
      class="minesWrapper__mine"
      :isMine="isMine"
      @click="handleMineClick"
      :style="{ background: activeColor }"
    ></div>

    <!-- <score v-if="gameFinished" :score="game.score" /> -->
  </div>
</template>

<script>
export default {
  props: ["isMine", "game"],
  data() {
    return {
      activeColor: "#ccc",
      gameFinished: false
    };
  },
  methods: {
    handleMineClick() {
      if (this.isMine) {
        // TODO
        this.activeColor = "red";

        this.gameFinished = true;

        this.$emit("showScore", this.game.score);
      } else {
        // TODO
        this.activeColor = "green";

        this.game.score += 5;
      }
    }
  },
  computed: {}
};
</script>

<style>
</style>