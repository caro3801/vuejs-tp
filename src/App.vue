<template>
  <div id="app">
       <b-form-select v-model="boardSize" :options="options" class="mb-3">
    </b-form-select>
    <!-- <div>Selected: <strong>{{ boardSize }}</strong></div> -->
    <Board v-if="randomChamps" :champions="randomChamps" :size="boardSize"/>
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
    options: [
      { value: 8, text: "8 elements" },
      { value: 12, text: "12 elements" },
      { value: 16, text: "16 elements" }
    ],
    randomChamps: [],
    boardSize: 12
  }),
  mounted: function() {
    this.getChampions();
  },
  watch: {
    boardSize: function() {
      this.randomChamps = this.randomChamps.slice(0, this.boardSize);
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
          for (let i = 0; i < this.boardSize / 2; i++) {
            let rand = Math.floor(Math.random() * Math.floor(nbChampions));
            let currentChamp = this.champions[rand];
            this.randomChamps.push({
              key: currentChamp.key + "_0",
              id: currentChamp.id,
              name: currentChamp.name,
              img: currentChamp.key + "_0.jpg",
              flipped: true
            });
            this.randomChamps.push({
              key: currentChamp.key + "_1",
              id: currentChamp.id,
              name: currentChamp.name,
              img: currentChamp.key + "_1.jpg",
              flipped: true
            });

            this.champions.splice(rand, 1);
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
