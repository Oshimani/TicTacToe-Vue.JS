<template>
  <div class="tictactoe">
   <div class="grid-container">
    <Field class="grid-item"/>  
    <Field class="grid-item"/>  
    <Field class="grid-item"/>  
    <Field class="grid-item"/>  
    <Field class="grid-item"/>  
    <Field class="grid-item"/>  
    <Field class="grid-item"/>  
    <Field class="grid-item"/>  
    <Field class="grid-item"/>  
   </div>
  </div>
</template>

<script>
import Field from "./Field";
export default {
  name: "TicTacToe",
  data() {
    return {
      msg: "Welcome to Your Vue.js App"
    };
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
