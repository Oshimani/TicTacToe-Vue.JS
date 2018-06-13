<template>
  <div id="app">
      <div class="header grid-container">
        <span class="score grid-item">
          <font-awesome-icon class="icon" :icon="iconFaTimes()"/>
          {{score[0]}}
        </span>
        <img class="header-image grid-item" src="./assets/logo.png">
        <span class="score grid-item">
          {{score[1]}}
          <font-awesome-icon class="icon" :icon="iconFaCircle()"/>          
        </span>
      </div>
      <TicTacToe v-on:new-score=handleScoreChanged></TicTacToe>
  </div>
</template>

<script>
import TicTacToe from "./components/TicTacToe";
import FontAwesomeIcon from "@fortawesome/vue-fontawesome";
import { faTimes, faCircle } from "@fortawesome/fontawesome-free-solid";

export default {
  name: "app",
  components: {
    TicTacToe,
    FontAwesomeIcon
  },
  data() {
    return {
      score: [0, 0]
    };
  },
  methods: {
    handleScoreChanged: function(score) {
      this.score = score;
      this.$forceUpdate();
    },
    iconFaTimes: function() {
      return faTimes;
    },
    iconFaCircle: function() {
      return faCircle;
    }
  }
};
</script>

<style>
body {
  overflow-y: scroll;
}
.score {
  font-size: 50px;
}
.header {
  position: fixed;
  z-index: 100;
  top: 0px;
  width: 100%;
  height: 203px;
  background-color: #42b983;
  border-bottom: 3px solid #2c3e50;
}
.header-image {
  filter: drop-shadow(5px 5px 5px #2c3e50);
}
.grid-container {
}
.grid-item {
}
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  text-align: center;
  margin-top: 213px;
}
</style>
