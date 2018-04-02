<template>
  <div class="tictactoe">
    <h3>Currently playing: {{currentPlayer}}</h3>
   <div class="grid-container">
    <Field v-bind:coords="[0,0]" class="grid-item" v-bind:currentPlayer="currentPlayer" v-bind:winnerTiles="winnerTiles" v-bind:allowClick="!gameOver" v-on:move-done="handleMoveDone"/>  
    <Field v-bind:coords="[0,1]" class="grid-item" v-bind:currentPlayer="currentPlayer" v-bind:winnerTiles="winnerTiles" v-bind:allowClick="!gameOver" v-on:move-done="handleMoveDone"/>  
    <Field v-bind:coords="[0,2]" class="grid-item" v-bind:currentPlayer="currentPlayer" v-bind:winnerTiles="winnerTiles" v-bind:allowClick="!gameOver" v-on:move-done="handleMoveDone"/>  
    <Field v-bind:coords="[1,0]" class="grid-item" v-bind:currentPlayer="currentPlayer" v-bind:winnerTiles="winnerTiles" v-bind:allowClick="!gameOver" v-on:move-done="handleMoveDone"/>  
    <Field v-bind:coords="[1,1]" class="grid-item" v-bind:currentPlayer="currentPlayer" v-bind:winnerTiles="winnerTiles" v-bind:allowClick="!gameOver" v-on:move-done="handleMoveDone"/>  
    <Field v-bind:coords="[1,2]" class="grid-item" v-bind:currentPlayer="currentPlayer" v-bind:winnerTiles="winnerTiles" v-bind:allowClick="!gameOver" v-on:move-done="handleMoveDone"/>  
    <Field v-bind:coords="[2,0]" class="grid-item" v-bind:currentPlayer="currentPlayer" v-bind:winnerTiles="winnerTiles" v-bind:allowClick="!gameOver" v-on:move-done="handleMoveDone"/>  
    <Field v-bind:coords="[2,1]" class="grid-item" v-bind:currentPlayer="currentPlayer" v-bind:winnerTiles="winnerTiles" v-bind:allowClick="!gameOver" v-on:move-done="handleMoveDone"/>  
    <Field v-bind:coords="[2,2]" class="grid-item" v-bind:currentPlayer="currentPlayer" v-bind:winnerTiles="winnerTiles" v-bind:allowClick="!gameOver" v-on:move-done="handleMoveDone"/>  
   </div>
  </div>
</template>

<script>
import Field from "./Field";
export default {
  name: "TicTacToe",
  data() {
    return {
      currentPlayer: 0,
      field: [
        [
          { coords: [0, 0], player: null },
          { coords: [0, 1], player: null },
          { coords: [0, 2], player: null }
        ],
        [
          { coords: [1, 0], player: null },
          { coords: [1, 1], player: null },
          { coords: [1, 2], player: null }
        ],
        [
          { coords: [2, 0], player: null },
          { coords: [2, 1], player: null },
          { coords: [2, 2], player: null }
        ]
      ],
      winnerTiles: []
    };
  },
  methods: {
    handleMoveDone: function(e) {
      // console.log(
      //   "Player: " +
      //     e.player +
      //     " placed on: [" +
      //     e.coords[0] +
      //     "][" +
      //     e.coords[1] +
      //     "]"
      // );
      this.field[e.coords[0]][e.coords[1]].player = e.player;
      this.currentPlayer = this.currentPlayer === 0 ? 1 : 0;
      // this.logFieldState();
      this.detectWinCondition(e);
    },
    detectWinCondition: function(e) {
      let winScenario = this.checkRow(e);
      if (winScenario.won) {
        console.warn("Player " + e.player + " won!");
        console.log(winScenario.tiles);
        this.winnerTiles = winScenario.tiles;
        return;
      }
      winScenario = this.checkCol(e);
      if (winScenario.won) {
        console.warn("Player " + e.player + " won!");
        console.log(winScenario.tiles);
        this.winnerTiles = winScenario.tiles;
        return;
      }
      winScenario = this.checkDiagTLBR(e);
      if (winScenario.won) {
        console.warn("Player " + e.player + " won!");
        console.log(winScenario.tiles);
        this.winnerTiles = winScenario.tiles;
        return;
      }
      winScenario = this.checkDiagBLTR(e);
      if (winScenario.won) {
        console.warn("Player " + e.player + " won!");
        console.log(winScenario.tiles);
        this.winnerTiles = winScenario.tiles;
        return;
      }
    },
    checkRow: function(e) {
      let numberOfSameLeft = -1;
      let numberOfSameRight = -1;
      let lenseCoords = [e.coords[0], e.coords[1]];
      let winnerTiles = [];
      // move lense left
      while (lenseCoords[1] >= 0) {
        // console.log(
        //   "Scanning: [" + lenseCoords[0] + "][" + lenseCoords[1] + "]"
        // );
        if (this.field[lenseCoords[0]][lenseCoords[1]].player === e.player) {
          numberOfSameLeft++;
          winnerTiles.push([lenseCoords[0], lenseCoords[1]]);
        }
        lenseCoords[1]--;
      }
      // center Lense
      lenseCoords = [e.coords[0], e.coords[1]];
      // move lende right
      while (lenseCoords[1] <= 2) {
        // console.log(
        //   "Scanning: [" + lenseCoords[0] + "][" + lenseCoords[1] + "]"
        // );
        if (this.field[lenseCoords[0]][lenseCoords[1]].player === e.player) {
          numberOfSameRight++;
          winnerTiles.push([lenseCoords[0], lenseCoords[1]]);
        }
        lenseCoords[1]++;
      }
      // console.log(
      //   "Found left: " + numberOfSameLeft + " Found right: " + numberOfSameRight
      // );
      if (numberOfSameLeft + numberOfSameRight > 1) {
        return { won: true, tiles: winnerTiles };
      } else {
        return { won: false };
      }
    },
    checkCol: function(e) {
      let numberOfSameTop = -1;
      let numberOfSameBot = -1;
      let lenseCoords = [e.coords[0], e.coords[1]];
      let winnerTiles = [];

      // move lense left
      while (lenseCoords[0] >= 0) {
        // console.log(
        //   "Scanning: [" + lenseCoords[0] + "][" + lenseCoords[1] + "]"
        // );
        if (this.field[lenseCoords[0]][lenseCoords[1]].player === e.player) {
          numberOfSameTop++;
          winnerTiles.push([lenseCoords[0], lenseCoords[1]]);
        }
        lenseCoords[0]--;
      }
      // center Lense
      lenseCoords = [e.coords[0], e.coords[1]];
      // move lende right
      while (lenseCoords[0] <= 2) {
        // console.log(
        //   "Scanning: [" + lenseCoords[0] + "][" + lenseCoords[1] + "]"
        // );
        if (this.field[lenseCoords[0]][lenseCoords[1]].player === e.player) {
          numberOfSameBot++;
          winnerTiles.push([lenseCoords[0], lenseCoords[1]]);
        }
        lenseCoords[0]++;
      }
      // console.log(
      //   "Found top: " + numberOfSameTop + " Found bot: " + numberOfSameBot
      // );
      if (numberOfSameTop + numberOfSameBot > 1) {
        return { won: true, tiles: winnerTiles };
      } else {
        return { won: false };
      }
    },
    checkDiagTLBR: function(e) {
      let numberOfSameTL = -1;
      let numberOfSameBR = -1;
      let lenseCoords = [e.coords[0], e.coords[1]];
      let winnerTiles = [];
      // move lense left
      while (lenseCoords[0] >= 0 && lenseCoords[1] >= 0) {
        // console.log(
        //   "Scanning: [" + lenseCoords[0] + "][" + lenseCoords[1] + "]"
        // );
        if (this.field[lenseCoords[0]][lenseCoords[1]].player === e.player) {
          numberOfSameTL++;
          winnerTiles.push([lenseCoords[0], lenseCoords[1]]);
        }
        lenseCoords[0]--;
        lenseCoords[1]--;
      }
      // center Lense
      lenseCoords = [e.coords[0], e.coords[1]];
      // move lende right
      while (lenseCoords[0] <= 2 && lenseCoords[1] <= 2) {
        // console.log(
        //   "Scanning: [" + lenseCoords[0] + "][" + lenseCoords[1] + "]"
        // );
        if (this.field[lenseCoords[0]][lenseCoords[1]].player === e.player) {
          numberOfSameBR++;
          winnerTiles.push([lenseCoords[0], lenseCoords[1]]);
        }
        lenseCoords[0]++;
        lenseCoords[1]++;
      }
      // console.log(
      //   "Found top-left: " +
      //     numberOfSameTL +
      //     " Found bot-right: " +
      //     numberOfSameBR
      // );
      if (numberOfSameTL + numberOfSameBR > 1) {
        return { won: true, tiles: winnerTiles };
      } else {
        return { won: false };
      }
    },
    checkDiagBLTR: function(e) {
      let numberOfSameBL = -1;
      let numberOfSameTR = -1;
      let lenseCoords = [e.coords[0], e.coords[1]];
      let winnerTiles = [];
      // move lense left
      while (lenseCoords[0] <= 2 && lenseCoords[1] >= 0) {
        console.log(
          "Scanning: [" + lenseCoords[0] + "][" + lenseCoords[1] + "]"
        );
        if (this.field[lenseCoords[0]][lenseCoords[1]].player === e.player) {
          numberOfSameBL++;
          winnerTiles.push([lenseCoords[0], lenseCoords[1]]);
        }
        lenseCoords[0]++;
        lenseCoords[1]--;
      }
      // center Lense
      lenseCoords = [e.coords[0], e.coords[1]];
      // move lende right
      while (lenseCoords[0] >= 0 && lenseCoords[1] <= 2) {
        console.log(
          "Scanning: [" + lenseCoords[0] + "][" + lenseCoords[1] + "]"
        );
        if (this.field[lenseCoords[0]][lenseCoords[1]].player === e.player) {
          numberOfSameTR++;
          winnerTiles.push([lenseCoords[0], lenseCoords[1]]);
        }
        lenseCoords[0]--;
        lenseCoords[1]++;
      }
      console.log(
        "Found bot-left: " +
          numberOfSameBL +
          " Found top-right: " +
          numberOfSameTR
      );
      if (numberOfSameBL + numberOfSameTR > 1) {
        return { won: true, tiles: winnerTiles };
      } else {
        return { won: false };
      }
    },
    logFieldState: function() {
      console.log("Field State:");
      for (let row = 0; row < this.field.length; row++) {
        console.log(
          "[" +
            this.field[row][0].player +
            "][" +
            this.field[row][1].player +
            "][" +
            this.field[row][2].player +
            "]"
        );
      }
    }
  },
  computed: {
    gameOver: function() {
      return this.winnerTiles.length > 0 ? true : false;
    }
  },
  components: {
    Field
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
a {
  color: #42b983;
}
.grid-container {
  display: inline-grid;
  grid-gap: 15px;
  grid-template-columns: auto auto auto;
  padding: 10px;
}
</style>
