<template>
  <page>
    <ActionBar title="Yellow Bucket" icon>
      <NavigationButton text="Back" android.systemIcon="ic_menu_back" @tap="goBack"/>
    </ActionBar>
      <ScrollView>        
        <StackLayout>        
          <movie-image :id="movieId"></movie-image>
          <Label horizontalAlignment="center" :text="Movie.title" textWrap="true" class="title"/>
          <Label horizontalAlignment="center" :text="'Rating: ' + Movie.rating" textWrap="true"/>
          <Label horizontalAlignment="center" :text="'Length: ' + Movie.length + ' min'" textWrap="true"/>
          <Label horizontalAlignment="center" :text="Movie.description" textWrap="true" class="description-label"/>
        </StackLayout>    
      </ScrollView>
  </page>
</template>
<script>
import MovieImage from "@/components/MovieComponents/MovieImage.vue";
import axios from "axios";
export default {
  data() {
    return {
      movieId: this.id,
      Movie: Object
    };
  },
  methods: {
    goBack() {
      this.$navigateBack();
    },
    getMovieData() {
      let url = "https://nathanielpadgett.info/api/movies/" + this.movieId;
      axios.get(url).then(result => {
        console.log(result.data);
        this.Movie = result.data;
        console.log(this.Movie.title);
      });
    }
  },
  mounted() {
    this.getMovieData();
  },
  components: {
    MovieImage
  },
  props: {
    id: Number
  }
};
</script>
<style scoped>
ActionBar {
  color: white;
  background-color:rgb(70, 67, 64);
  
}
StackLayout {
  background-color: rgb(224, 224, 224);
}
Label {
  color: black;
  font-size: 15;
  text-align: center;
}
.description-label {
  margin: 20;
}
.title {
  font-size: 20;
}
</style>
