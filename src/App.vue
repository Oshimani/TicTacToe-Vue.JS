<template>
  <div id="app">
      <div class="header">
        <img class="header-image" src="./assets/logo.png">
      </div>
      <TicTacToe></TicTacToe>
  </div>
</template>

<script>
import TicTacToe from "./components/TicTacToe";

export default {
  name: "app",
  components: {
    TicTacToe
  }
};
</script>

<style>
body{
  overflow-y: scroll;
}
.header {
  position: fixed;
  z-index: 100;
  top: 0px;
  width:100%;
  height: 203px;
  background-color: #42b983;
  border-bottom: 3px solid #2c3e50;
}
.header-image{
  filter: drop-shadow(5px 5px 5px #2c3e50);
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
