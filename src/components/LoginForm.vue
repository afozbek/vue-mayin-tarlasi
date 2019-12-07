<template>
  <div class="m-loginForm">
    <div>
      <div class="m-loginForm__wrapper">
        <label for="name">Name:</label>
        <input class="a-input" type="text" id="name" name="surname" v-model="name" />
      </div>

      <div class="m-loginForm__wrapper">
        <label for="surname">Surname:</label>
        <input class="a-input" type="text" id="surname" name="surname" v-model="surname" />
      </div>

      <button @click="startGame" class="m-loginForm__button">Start Game</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "",
  data() {
    return {
      name: "",
      surname: ""
    };
  },
  methods: {
    startGame() {
      console.log("Starting the game..");

      this.$emit("gameStarted", {
        name: this.name,
        surname: this.surname
      });
    }
  }
};
</script>

<style lang="scss">
.m-loginForm {
  display: flex;
  justify-content: center;
  flex-direction: column;
  align-items: center;

  & > * {
    margin-bottom: 10px;
  }

  // &__wrapper {
  //   width: 40%;
  // }

  &__button {
    width: 100px;
  }
}
</style>
