<template>
    <StackLayout >      
      <Image height="400" horizontalAlignment="center" :src="imgUrl" stretch="aspectFit"/>
    </StackLayout>
</template>
<script>
export default {
  data() {
    return {};
  },
  computed: {
    imgUrl: function() {
      return "https://nathanielpadgett.info/images/movie_" + this.id + ".jpg";
    }
  },
  props: {
    id: Number
  }
};
</script>
<style scoped>
  Image {
    margin: 10;
    border-radius: 20;

  }
</style>
