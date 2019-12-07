<template>
  <div>
    <h1>Scores</h1>

    <ol>
      <li v-for="score in scoreBoard">Score: {{score.person.name}} - {{score.score}}</li>
    </ol>
  </div>
</template>

<script>
export default {
  props: ["scoreBoard"]
};
</script>

<style>
</style>