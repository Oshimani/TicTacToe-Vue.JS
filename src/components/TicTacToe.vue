<template>
    <div>
        <div class="board-list">
            <Board class="board" v-for="board in boards" v-bind:key="board.index"></Board>
        </div>
        <div class="footer">
            <button class="button" v-on:click="clickNewGame()">Neues Spiel</button>
        </div>
    </div>
</template>

<script>
import Board from "./Board";

export default {
  name: "TicTacToe",
  components: {
    Board
  },
  data() {
    return {
        index:1,
      boards: [{index:0}]
    };
  },
  methods: {
    clickNewGame: function() {
      console.log("New Game");
      this.boards.unshift({index:this.index});
      this.index++;
    }
  }
};
</script>

<style>
.board:not(:first-of-type){
    /* background-color: #c4c4c4; */
    filter: blur(2px);
}
.board:first-of-type{
    border-bottom: 3px solid #2c3e50;
}
.button {
  border-radius: 5px;
  border: 3px solid #348f66;
  background-color: #42b983;
  color: #2c3e50;
  font-size: 25px;
}
.button:hover {
  transform: scale(1.1);
  cursor: pointer;
  background-color: #2c3e50;
  color: #42b983;
}
.board-list{
    margin-bottom: 68px;
}
.footer{
    position:fixed;
    bottom: 0px;
    background-color: #42b983;
    border-top: 3px solid #2c3e50;
    width:100%;
    padding: 10px;
}
</style>
