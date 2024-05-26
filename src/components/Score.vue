<template>
  <div>
    <div v-if="gameOver">
      <p v-if="winner">Player {{ winner }} wins!</p>
      <p v-else>It's a tie!</p>
      <p>{{ player1 }} :{{ score.player1 }}</p>
      <p>{{ player2 }} :{{ score.player2 }}</p>
      <button @click="startNewGame">Start New Game</button>
      <button @click="playAgain">Play Again</button>
    </div>
    <div v-else>
      <h3></h3>
      <p>Current Player: {{ currentPlayer }}</p>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    player1: String,
    player2: String,
    currentPlayer: String,
    gameOver: Boolean,
    winner: String,
    score: Object,
  },
  methods: {
    startNewGame() {
      this.$emit("start-new-game");
    },
    playAgain() {
      this.$emit("play-again");
    },
  },
};
</script>

<style scoped></style>
