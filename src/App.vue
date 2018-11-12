<template>
  <div id="app">
    <Board v-if="champions" :champions = "champions"/>
    {{getRandomChampions}}
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
    boardSize: 16
  }),
  mounted: function() {
    this.getChampions();
  },
  computed: {
    getRandomChampions: function() {
      function getRandomInt(max) {
        return Math.floor(Math.random() * Math.floor(max));
      }
      let nbChampions = this.champions.length;
      let selectedChampions = [];
      for (let i; i < this.boardSize; i++) {
        let rand = getRandomInt(nbChampions);
        selectedChampions.push(this.champions[rand]);
        this.champions.slice(rand, rand + 1);
        --nbChampions;
      }
      return selectedChampions;
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
