<template>
  <ListView for="movie in moviesArray">
    <v-template>
      <FlexboxLayout flexDirection="column">
<StackLayout>
            <movie-image row="0" :id="movie.id"></movie-image>
          <Label :text="movie.title" row="1" col="1" colSpan="2" horizontalAlignment="center" class="text-field" height/>
          <Label
            :text="'Rating: ' + movie.rating"
            row="2"
            col="1"
            colSpan="2"
            class="text-field"
            height
            horizontalAlignment="center"
          />
          <movie-buttons horizontalAlignment="center" :id="movie.id" :movieTitle="movie.title"></movie-buttons>
</StackLayout>
      </FlexboxLayout>
    </v-template>
  </ListView>
</template>
<script>
import MovieImage from "@/components/MovieComponents/MovieImage.vue";
import MovieButtons from "@/components/MovieComponents/MovieButtons.vue";
export default {
  data() {
    return {
      moviesArray: this.movies
    };
  },
  methods: {
    DetailsTap(id) {
      console.log("this is the Details button");
    },
    RenteesTap(id) {
      console.log("This is the rentees button");
    }
  },
  mounted() {
    console.log(this.moviesArray);
  },
  props: ["movies"],
  components: {
    MovieImage,
    MovieButtons
  }
};
</script>
<style scoped>
.text-field {
  color: black;
  font-size: 20;
  vertical-align: center;
}
ListView {
  background-color:rgb(224, 224, 224);
  margin: 20;
}
</style>
