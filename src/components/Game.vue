<template>
  <section class="game">
    <div class="scores-container">
      <h3 class="player1">{{ player1 }}:{{ score.player1 }}</h3>
      <h3 class="player2">{{ player2 }}:{{ score.player2 }}</h3>
    </div>

    <div v-if="!gameOver">
      <div>
        <p>Current Player: {{ currentPlayer }}</p>
      </div>
      <div class="board">
        <div
          class="square"
          v-for="item in items"
          :key="item.id"
          @click="handleClick(item.id)"
        >
          <span
            :style="{ color: item.value === 'X' ? player1Color : player2Color }"
          >
            {{ item.value }}
          </span>
        </div>
      </div>
    </div>

    <div v-if="gameOver">
      <Score
        :player1="player1"
        :player2="player2"
        :currentPlayer="currentPlayer"
        :gameOver="gameOver"
        :winner="winner"
        :score="score"
        @start-new-game="startNewGame"
        @play-again="playAgain"
      />
    </div>
  </section>
</template>

<script>
import { defineComponent } from "vue";
import Score from "./Score.vue";

export default defineComponent({
  components: {
    Score,
  },
  props: {
    player1: String,
    player2: String,
    player1Color: String,
    player2Color: String,
  },
  data() {
    return {
      currentPlayer: this.player1,
      items: [
        { id: "item1", value: "" },
        { id: "item2", value: "" },
        { id: "item3", value: "" },
        { id: "item4", value: "" },
        { id: "item5", value: "" },
        { id: "item6", value: "" },
        { id: "item7", value: "" },
        { id: "item8", value: "" },
        { id: "item9", value: "" },
      ],
      gameOver: false,
      winner: null,
      score: {
        player1: 0,
        player2: 0,
      },
    };
  },
  methods: {
    handleClick(id) {
      if (!this.gameOver) {
        let square = this.items.find((item) => item.id === id);

        if (square.value === "") {
          square.value = this.currentPlayer === this.player1 ? "X" : "O";
          this.checkWinner();
          if (!this.gameOver) {
            this.currentPlayer =
              this.currentPlayer === this.player1 ? this.player2 : this.player1;
          }
        }
      }
    },
    checkWinner() {
      const lines = [
        [0, 1, 2],
        [3, 4, 5],
        [6, 7, 8],
        [0, 3, 6],
        [1, 4, 7],
        [2, 5, 8],
        [0, 4, 8],
        [2, 4, 6],
      ];
      for (let line of lines) {
        const [a, b, c] = line;
        if (
          this.items[a].value &&
          this.items[a].value === this.items[b].value &&
          this.items[a].value === this.items[c].value
        ) {
          this.winner = this.currentPlayer;
          this.gameOver = true;
          this.updateScore();
          return;
        }
      }
      if (this.items.every((item) => item.value !== "")) {
        this.gameOver = true;
        return;
      }
    },
    updateScore() {
      if (this.winner === this.player1) {
        this.score.player1++;
      } else if (this.winner === this.player2) {
        this.score.player2++;
      }
    },
    startNewGame() {
      this.$emit('reset-game');
    },
    playAgain() {
      this.items.forEach((item) => {
        item.value = "";
      });
      this.currentPlayer = this.player1;
      this.gameOver = false;
      this.winner = null;
    },
  },
});
</script>

<style scoped>
.scores-container {
  position: fixed;
  top: 20px;
  left: 20px;
  display: flex;
  justify-content: space-between;
  width: calc(100% - 40px);
  z-index: 999;
}

.player1,
.player2 {
  margin: 0;
  padding: 0 10px;
}

.player2 {
  order: 1;
}

.board {
  display: grid;
  grid-template-columns: repeat(3, 80px);
  grid-template-rows: repeat(3, 80px);
  gap: 5px;
  margin: 20px auto;
}

.square {
  line-height: 80px;
  text-align: center;
  font-size: 2rem;
  background-color: blueviolet;
  color: white;
  cursor: pointer;
}

.square:hover {
  background-color: black;
}
</style>
