<template>
  <div class="game-body">
    <div class="game-status">{{ gameStatus }}</div>
    <game-board :tics="tics" :OnHandleClick="OnClicked"></game-board>
    <button v-if="isResetEnabled" @click="reset()">Reset</button>
  </div>
</template>

<script>
import GameBoard from "./Board.vue";

export default {
  name: "Game",
  components: {
    GameBoard
  },
  data: function() {
    return {
      winner: null,
      isPlayerX: true,
      tics: Array(9).fill("")
    };
  },
  computed: {
    gameStatus: function() {
      if (this.winner === "X" || this.winner === "O") {
        return "Winner is " + this.winner;
      }

      if (this.isPlayerX) {
        return "Next Player: X";
      } else {
        return "Next Player: O";
      }
    },
    isResetEnabled: function() {
      if (this.winner === "X" || this.winner === "O") {
        return true;
      }
      for (let i = 0; i < this.tics.length; i++) {
        if (this.tics[i] != "X" && this.tics[i] != "O") {
          return false;
        }
      }

      return true;
    }
  },
  methods: {
    calculateWinner() {
      const lines = [
        [0, 1, 2],
        [3, 4, 5],
        [6, 7, 8],
        [0, 3, 6],
        [1, 4, 7],
        [2, 5, 8],
        [0, 4, 8],
        [2, 4, 6]
      ];

      for (let i = 0; i < lines.length; i++) {
        const [a, b, c] = lines[i];
        if (
          this.tics[a] &&
          this.tics[a] === this.tics[b] &&
          this.tics[b] === this.tics[c]
        ) {
          this.winner = this.tics[a];
          return;
        }
      }
    },
    OnClicked(i) {
      if (this.winner === "X" || this.winner === "O") {
        return;
      }

      if (this.tics[i] === "X" || this.tics[i] === "O") {
        return;
      }

      this.$set(this.tics, i, this.isPlayerX ? "X" : "O");
      this.isPlayerX = !this.isPlayerX;
      this.calculateWinner();
      console.log("index " + i + " is " + this.tics[i]);
    },
    reset() {
      console.log("reset");
      for (let i = 0; i < this.tics.length; i++) {
        this.$set(this.tics, i, "");
      }
      this.winner = null;
    }
  }
};
</script>
