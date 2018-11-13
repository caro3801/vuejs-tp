<template>

    <div class="row" >
           
           <Card v-for="card in champions" :key="card.key" :src="card.img" :name="card.name"/>
         
        </div>    
</template>  
<script>
import Card from "./Card.vue";
export default {
  name: "Board",
  components: {
    Card
  },

  props: {
    champions: Array,
    size: Number
  },
  data: () => ({
    cards: []
  }),

  methods: {
    initDeck() {},
    flipSelectedCard(cardPosition) {
      let flippedChampion = {
        ...this.state.champions[cardPosition],
        flipped: !this.state.champions[cardPosition].flipped
      };
      let champs = this.state.champions;
      champs.splice(cardPosition, 1, flippedChampion);
      return champs;
    },
    handleClick(cardPosition, event) {
      if (this.state.firstCardFlipped === null) {
        let champs = this.flipSelectedCard(cardPosition);
        this.setState({ champions: champs, firstCardFlipped: cardPosition });
      } else if (
        this.state.secondCardFlipped === null &&
        this.state.firstCardFlipped !== cardPosition
      ) {
        let champs = this.flipSelectedCard(cardPosition);
        this.setState({ champions: champs, secondCardFlipped: cardPosition });
        setTimeout(this.hideCardsWhenDifferent.bind(this), 1000);
      }
    },
    shuffle(a) {
      for (let i = a.length - 1; i > 0; i--) {
        const j = Math.floor(Math.random() * (i + 1));
        [a[i], a[j]] = [a[j], a[i]];
      }
      return a;
    }
  }
};
</script>
