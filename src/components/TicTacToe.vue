<template>
  <div class="tictactoe">
    <h3>Currently playing: {{currentPlayer}}</h3>
   <div class="grid-container">
    <Field class="grid-item" v-bind:currentPlayer="currentPlayer" v-on:move-done="handleMoveDone()"/>  
    <Field class="grid-item" v-bind:currentPlayer="currentPlayer" v-on:move-done="handleMoveDone()"/>  
    <Field class="grid-item" v-bind:currentPlayer="currentPlayer" v-on:move-done="handleMoveDone()"/>  
    <Field class="grid-item" v-bind:currentPlayer="currentPlayer" v-on:move-done="handleMoveDone()"/>  
    <Field class="grid-item" v-bind:currentPlayer="currentPlayer" v-on:move-done="handleMoveDone()"/>  
    <Field class="grid-item" v-bind:currentPlayer="currentPlayer" v-on:move-done="handleMoveDone()"/>  
    <Field class="grid-item" v-bind:currentPlayer="currentPlayer" v-on:move-done="handleMoveDone()"/>  
    <Field class="grid-item" v-bind:currentPlayer="currentPlayer" v-on:move-done="handleMoveDone()"/>  
    <Field class="grid-item" v-bind:currentPlayer="currentPlayer" v-on:move-done="handleMoveDone()"/>  
   </div>
  </div>
</template>

<script>
import Field from "./Field";
export default {
  name: "TicTacToe",
  data() {
    return {
      currentPlayer: 0
    };
  },
  methods: {
    handleMoveDone: function() {
      // console.log("Move done");
      this.currentPlayer = this.currentPlayer === 0 ? 1 : 0;
    }
  },
  computed: {},
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
