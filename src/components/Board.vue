<template>
    <div class="row" >
           
           <Card v-for="champion in champions" :key="champion.name" :src="champion.src" :name="champion.name"/>
         
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
    champions: Array
  },
  methods: {
    created() {
      console.log("hello");
    }
  }
};
</script>
