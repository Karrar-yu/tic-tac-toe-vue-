<template>
  <div>
    <section v-if="!gameStarted" class="playerStart">
      <div class="player2">
        <label>Player 1</label>
        <input type="text" v-model="player1" required />
      </div>
      <div class="player1">
        <label>Player 2</label>
        <input type="text" v-model="player2" required />
      </div>
      <button @click="startGame">Start</button>
    </section>

    <section v-else class="game">
      <Game
        :player1="player1"
        :player2="player2"
        :player1Color="'lightgreen'"
        :player2Color="'red'"
      />
    </section>
  </div>
</template>

<script>
import { defineComponent } from "vue";
import Game from "./Game.vue";

export default defineComponent({
  components: {
    Game,
  },
  data() {
    return {
      player1: "",
      player2: "",
      gameStarted: false,
    };
  },
  methods: {
    startGame() {
      if (this.player1 !== "" && this.player2 !== "") {
        this.gameStarted = true;
      } else {
        alert("Please enter both player names.");
      }
    },
  },
});
</script>

<style scoped>
.playerStart {
  text-align: center;
  display: flex;
  flex-direction: column;
  align-items: center;
  font-size: 1.5rem;
}
.playerStart label,
input {
  margin: 10px 10px;
  font-size: 1.2rem;
  display: flex;
}

.game {
  position: relative;
  width: 255px;
  margin: auto;
  font-size: 2rem;
  text-align: center;
}
</style>
