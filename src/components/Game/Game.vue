<template>
  <div class="game-wrapper">
    <div class="game-header">
      <div>
        Name:
        <strong>{{person.name}} {{person.surname}}</strong>
      </div>

      <div>
        Score:
        <strong>{{game.score}}</strong>
      </div>

      <button @click="restartGame($event)">Restart The Game</button>
    </div>

    <div style="display: flex;">
      <div class="minesWrapper">
        <mine
          :key="mine.id"
          v-for="mine in mines"
          :isMine="mine.isMine"
          :game="game"
          @showScore="showScore($event)"
        ></mine>
      </div>

      <slot></slot>
    </div>

    <score v-if="gameFinished" :score="game.score" @handleFailed="restartGame" />
    <!-- <div class="scores">SCORES</div> -->
  </div>
</template>

<script>
import Mine from "@/components/Game/Mine.vue";
import Score from "@/components/Game/Score.vue";

export default {
  props: ["person"],
  components: {
    Mine,
    Score
  },
  data() {
    return {
      game: {
        score: 0
      },
      mineCount: 25,
      mines: [],
      gameFinished: false
    };
  },
  methods: {
    restartGame() {
      console.log("Restarting the game..");
      this.gameFinished = false;

      this.$emit("gameRestarted");
    },
    showScore(score) {
      console.log("Showing Score");
      this.gameFinished = true;

      alert("Your Score: " + this.game.score);

      this.$emit("addScore", { person: this.person, score: this.game.score });
    }
  },
  created() {
    let count = 0;
    while (count !== this.mineCount) {
      let random = Math.random();
      this.mines.push({ isMine: random >= 0.5, id: Math.random() });
      count++;
    }
  }
};
</script>

<style lang="scss">
.minesWrapper {
  display: flex;
  flex-wrap: wrap;
  width: 350px;
  margin: 0 auto;

  &__mine {
    width: 50px;
    height: 50px;
    background: #ccc;
    margin: 10px;
  }
}

.game-wrapper {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.game-header {
  display: flex;
  justify-content: space-between;
  width: 43%;
}
</style>