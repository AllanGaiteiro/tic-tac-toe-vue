<template>
  <div id="app">
    <div class="status">{{ status }}</div>
    <button>Reset</button>
    <template v-for="(row, rowIndex) in board" :key="rowIndex">
      <div class="row">
        <button v-for="(col, colIndex) in board[rowIndex]" :key="`${rowIndex}-${colIndex}`" class="square"
          @click="$event => handleClick(rowIndex, colIndex)" :disabled="board[rowIndex][colIndex] !== null"
          style="width:40px;height:40px;">
          {{ board[rowIndex][colIndex] }}
        </button>

      </div>
    </template>
  </div>
</template>


<script>
export default {
  name: "App",
  data() {
    return {
      status: 'Next player: X',
      board: [
        [null, null, null],
        [null, null, null],
        [null, null, null]
      ],
      currentPlayer: 'X'
    };
  },
  methods: {
    handleClick(row, col) {
      if (this.board[row][col] !== null) {
        return; // Return early if the square is already filled
      }
      this.board[row][col] = this.currentPlayer;
      if (this.checkForWinner()) {
        this.status = `${this.currentPlayer} wins!`;
        return;
      }
      if (this.checkForDraw()) {
        this.status = `Game ended in a draw.`;
        return;
      }
      this.currentPlayer = this.currentPlayer === 'X' ? 'O' : 'X';
      this.status = `Next player: ${this.currentPlayer}`;
    },
    checkForWinner() {
      // Check rows
      for (let row = 0; row < 3; row++) {
        if (
          this.board[row][0] === this.currentPlayer &&
          this.board[row][1] === this.currentPlayer &&
          this.board[row][2] === this.currentPlayer
        ) {
          return true;
        }
      }
      // Check columns
      for (let col = 0; col < 3; col++) {
        if (
          this.board[0][col] === this.currentPlayer &&
          this.board[1][col] === this.currentPlayer &&
          this.board[2][col] === this.currentPlayer
        ) {
          return true;
        }
      }
      // Check diagonals
      if (
        this.board[0][0] === this.currentPlayer &&
        this.board[1][1] === this.currentPlayer &&
        this.board[2][2] === this.currentPlayer
      ) {
        return true;
      }
      if (
        this.board[0][2] === this.currentPlayer &&
        this.board[1][1] === this.currentPlayer &&
        this.board[2][0] === this.currentPlayer
      ) {
        return true;
      }
      return false;
    },
    checkForDraw() {
      for (let row = 0; row < 3; row++) {
        for (let col = 0; col < 3; col++) {
          if (this.board[row][col] === null) {
            return false; // Game is not over if there is an empty square
          }
        }
      }
      return true; // All squares are filled, game is a draw
    },
    reset() {
      this.status = 'Next player: X';
      this.board = [
        [null, null, null],
        [null, null, null],
        [null, null, null]
      ];
      this.currentPlayer = 'X';
    }
  }
};
</script>


<style>
#app {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  font-family: Arial, sans-serif;
}

.status {
  margin-bottom: 1em;
  font-size: 18px;
  font-weight: bold;
}

.row {
  display: flex;
  justify-content: center;
}

.square {
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 24px;
  font-weight: bold;
  margin: 4px;
  background-color: white;
  border: 2px solid black;
  cursor: pointer;
}

.square:hover {
  background-color: lightgray;
}

button {
  padding: 8px 16px;
  border-radius: 4px;
  background-color: blue;
  color: black;
  font-size: 16px;
  font-weight: bold;
  border: none;
  cursor: pointer;
  margin-bottom: 1em;
}

button:hover {
  background-color: darkblue;
}
</style>