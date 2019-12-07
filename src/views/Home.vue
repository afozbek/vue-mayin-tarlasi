<template>
  <div class="home">
    <img src="@/assets/logo.svg" alt="Mayın Tarlası" />

    <login-form v-if="!gameStarted" @gameStarted="handleGameStart($event)"></login-form>

    <game v-else :person="person" @gameRestarted="handleGameRestart" @addScore="addScore($event)">
      <scores :scoreBoard="scoreBoard" />
    </game>
  </div>
</template>

<script>
// @ is an alias to /src
import LoginForm from "@/components/LoginForm.vue";
import Game from "@/components/Game/Game.vue";
import Scores from "@/components/Game/Scores.vue";

export default {
  name: "home",
  data() {
    return {
      person: {},
      gameStarted: false,
      scoreBoard: []
    };
  },
  components: {
    LoginForm,
    Game,
    Scores
  },
  methods: {
    handleGameStart(person) {
      this.person = person;
      this.gameStarted = true;
    },
    handleGameRestart() {
      this.gameStarted = false;
    },
    addScore(event) {
      this.scoreBoard.push(event);

      this.scoreBoard.sort((a, b) => b.score - a.score);

      if (this.scoreBoard.length > 10) {
        this.scoreBoard = this.scoreBoard.slice(0, 10);
      }

      this.gameStarted = false;
    }
  }
};
</script>
