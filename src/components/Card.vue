<template>
<b-card img-src="https://picsum.photos/600/300/?image=25"
          img-alt="Image"
          img-top
          tag="article"
          style="max-width: 20rem;"
          class="mb-2">
                <a class="thumbnail" href="#">
                    <img class="img-responsive" :src="src" alt="">
                    <div class="champName">{{championName}}</div> 
                </a>
            </b-card>
</template>


<script>
export default {
  name: "Card",
  props: {
    src: String,
    championName: String
  }
};
</script>
