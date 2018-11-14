<template>

    <div class="row" >
           
           <Card v-for="(card,index) in champions" :key="index" :src="card.img" :name="card.name" :isFlipped="card.flipped" v-on:click.native="handleClick(index,card.key,card.id)"/>
         
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
    firstCardFlippedId: null,
    secondCardFlippedId: null
  }),
  methods: {
    flipSelectedCard(cardPosition) {
      this.champions[cardPosition].flipped = !this.champions[cardPosition]
        .flipped;
    },
    handleClick: function(index, key, id) {
      if (this.firstCardFlippedId == null) {
        this.firstCardFlippedId = { key, id, index };
        this.flipSelectedCard(index);
      } else if (
        this.secondCardFlippedId == null &&
        this.firstCardFlippedId.key != key
      ) {
        this.secondCardFlippedId = { key, id, index };
        this.flipSelectedCard(index);
        setTimeout(this.hideCardsWhenDifferent, 1000);
      }
    },
    hideCardsWhenDifferent: function() {
      if (this.secondCardFlippedId.id !== this.firstCardFlippedId.id) {
        this.champions[this.firstCardFlippedId.index].flipped = !this
          .firstCardFlippedId.flipped;
        this.champions[this.secondCardFlippedId.index].flipped = !this
          .secondCardFlippedId.flipped;
      }
      this.firstCardFlippedId = null;
      this.secondCardFlippedId = null;
    }
  }
};
</script>
