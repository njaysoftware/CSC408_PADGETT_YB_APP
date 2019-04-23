<template>
  <StackLayout>  
      <Button class="first-button" text="Details" horizontalAlignment="center" @tap="DetailsTap(movieId)"/>
      <Button class="second-button" text="Rentees" horizontalAlignment="center" col="1" colspan="2" row="1" @tap="RenteesTap(movieId, movieTitle)"/>
  </StackLayout>
</template>
<script>
import MovieDetail from "@/components/MovieComponents/MovieDetails.vue";
import MovieRentees from "@/components/MovieComponents/MovieRentees.vue";
export default {
  data() {
    return {};
  },
  methods: {
    DetailsTap(ids) {
      this.$navigateTo(MovieDetail, { props: { id: ids } });
    },
    RenteesTap(ids, movieTitle) {
      this.$navigateTo(MovieRentees, { props: { id: ids, movieTitle: movieTitle} });
    }
  },
  computed: {
    movieId: function() {
      return this.id;
    }
  },
  props: {
    id: Number,
    movieTitle: String
  }
};
</script>
<style scoped>
.first-button {
  margin-top: 20;
}
.second-button {
  margin-bottom: 20;
}
Button 
{
  width: 50%;
  background-color: rgb(70, 67, 64);
  color: white;
}
</style>
