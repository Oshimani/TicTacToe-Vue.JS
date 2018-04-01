<template>
    <div v-bind:class="{'clicked': player !== null}"
        v-on:click="click()"
        @mouseover="hover = true"
        @mouseleave="hover = false"
        class="field">
        <font-awesome-icon v-if="player !== null" class="icon" :icon="iconFaTimes()"/>
        <font-awesome-icon v-if="hover && player === null" class="icon icon-dark" :icon="iconFaTimes()"/>
    </div>
</template>
<script>
import FontAwesomeIcon from "@fortawesome/vue-fontawesome";
import {
  faTimes,
  faCircle,
  faTimesCircle
} from "@fortawesome/fontawesome-free-solid";
export default {
  name: "Field",
  data() {
    return {
      player: null,
      hover: false
    };
  },
  methods: {
    click: function() {
      console.log("Clicked this tile");
      this.player = true;
    },
    iconFaTimes: function() {
      return faTimes;
    },
    iconFaCircle: function() {
      return faCircle;
    }
  },
  computed: {},
  components: {
    FontAwesomeIcon
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.field {
  background-color: #42b983;
  height: 150px;
  width: 150px;
  border: 3px solid #348f66;
  border-radius: 5px;
}
.field:not(.clicked):hover {
  transform: scale(1.1);
}
.clicked {
  background-color: #2c3e50;
}
.icon {
  color: #42b983;
  font-size: 120px;
  position: relative;
  top: 50%;
  transform: translate(0%, -50%);
}
.icon-dark {
  color: #2c3e50;
}
</style>
