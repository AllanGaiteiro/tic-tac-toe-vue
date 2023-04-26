<template>
  <div id="app">
    <div class="status">{{ status }}</div>
    <button>Reset</button>
    <template v-for="(row, rowIndex) in board" :key="rowIndex">
      <div class="row">
        <button v-for="(col, colIndex) in board[rowIndex]" class="square" style="width:40px;height:40px;"
          :key="`${rowIndex}-${colIndex}`" @click="$event => handleClick(rowIndex, colIndex)">{{ board[rowIndex][colIndex]
          }}</button>
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
      ]
    };
  },
  methods: {
    handleClick(row, col) {
      console.log(row, col)
    }
  }
};
</script>