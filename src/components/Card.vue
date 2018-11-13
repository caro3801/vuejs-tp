<template>
<b-card :img-src="'http://ddragon.leagueoflegends.com/cdn/img/champion/splash/'+src"
          img-alt="Image"
          img-top
          style="max-width: 18rem;"
          class="mb-2">
                <a class="thumbnail" href="#">
                    <div class="champName">{{name}}</div> 
                </a>
</b-card>
</template>


<script>
export default {
  name: "Card",
  props: {
    src: String,
    name: String
  }
};
</script>
