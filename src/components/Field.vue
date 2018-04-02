<template>
    <div v-bind:class="{'clicked': player !== null, 'winner': this.winner, 'disabled': !this.allowClick && !this.winner}"
        v-on:click="click()"
        @mouseover="mouseEnter"
        @mouseleave="hover = false"
        class="field">
        <!-- Player 0 Icon -->
        <font-awesome-icon v-if="player === 0" class="icon" :icon="iconFaTimes()"/>
        <!-- Player 0 Hover Icon -->
        <font-awesome-icon v-if="hover && player === null && currentPlayer === 0" class="icon icon-dark" :icon="iconFaTimes()"/>
        <!-- Player 1 Icon -->
        <font-awesome-icon v-if="player === 1" class="icon" :icon="iconFaCircle()"/>
        <!-- Player 1 Hover Icon -->
        <font-awesome-icon v-if="hover && player === null && currentPlayer === 1" class="icon icon-dark" :icon="iconFaCircle()"/>
        
        
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
  props: ["currentPlayer", "coords", "winnerTiles", "allowClick"],
  data() {
    return {
      player: null,
      hover: false
    };
  },
  methods: {
    click: function() {
      if (!this.allowClick) return;
      // console.log("Clicked this tile");
      this.player = this.currentPlayer;
      this.$emit("move-done", { player: this.player, coords: this.coords });
    },
    mouseEnter: function() {
      if (this.allowClick) this.hover = true;
    },
    iconFaTimes: function() {
      return faTimes;
    },
    iconFaCircle: function() {
      return faCircle;
    }
  },
  computed: {
    winner: function() {
      if (this.winnerTiles === undefined) return false;
      console.log(this.winnerTiles);
      return this.winnerTiles.findIndex(
        wt => wt[0] === this.coords[0] && wt[1] === this.coords[1]
      ) > -1
        ? true
        : false;
    }
  },
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
.field:not(.clicked):not(.disabled):hover {
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
.winner .icon {
  color: crimson !important;
}
.disabled {
  transform: scale(0.9);
}
</style>
