<template>
  <div id="app">
    <Board v-if="randomChamps" :champions = "randomChamps"/>
  
  </div>
</template>

<script>
import Board from "@/components/Board.vue";

export default {
  name: "app",
  components: {
    Board
  },
  data: () => ({
    champions: [],
    randomChamps: [],
    boardSize: 16
  }),
  mounted: function() {
    this.getChampions();
  },
  watch: {
    champions: function() {
      let nbChampions = this.champions.length;
      for (let i; i < this.boardSize; i++) {
        let rand = Math.floor(Math.random() * Math.floor(nbChampions));
        this.randomChamps.push(this.champions[rand]);
        this.champions.slice(rand, rand + 1);
        --nbChampions;
      }
    }
  },
  methods: {
    getChampions: function() {
      fetch("champions.json")
        .then(response => response.json())
        .then(response => {
          for (let champion in response.data) {
            this.champions.push(response.data[champion]);
          }
        })
        .then(() => {
          let nbChampions = this.champions.length;
          for (let i = 0; i < this.boardSize; i++) {
            let rand = Math.floor(Math.random() * Math.floor(nbChampions));
            this.randomChamps.push(this.champions[rand]);
            this.champions.slice(rand, rand + 1);
            --nbChampions;
          }
        })
        .catch(new Error("hello"));
    }
  }
};
</script>

<style lang="scss">
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
