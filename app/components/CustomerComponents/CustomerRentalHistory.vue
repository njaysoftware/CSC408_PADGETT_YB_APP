<template>
  <FlexboxLayout flexDirection="row" class="list-group-item">
    <GridLayout rows="*, *, *, *" columns="3*, 7*" width="100%">
      <Image :src="imageUrl" row="0" col="0" rowSpan="4" class="thumbnail"/>
      <Label :text="this.rental.title" row="0" col="1" class="label-text"/>
      <Label :text="this.rental.rating" row="1" col="1" class="label-text"/>
      <Label :text="'Rented: ' + rented" row="2" col="1" class="label-text"/>
      <Label :text="'Renturned: ' + returned" row="3" col="1" class="label-text"/>
    </GridLayout>
  </FlexboxLayout>
</template>
<script>
export default {
  data() {
    return {};
  },
  computed: {
    imageUrl: function() {
      return (
        "https://nathanielpadgett.info/images/movie_" +
        this.rental.transaction.movie_id +
        ".jpg"
      );
    },
    rented: function() {
      var options = { year: "numeric", month: "numeric", day: "numeric" };
      var day = new Date(this.rental.transaction.rent_date);
      return day.getMonth() + 1 + "/" + day.getDate() + "/" + day.getFullYear();
    },
    returned: function() {
      var options = { year: "numeric", month: "numeric", day: "numeric" };
      var day = new Date(this.rental.transaction.return_date);
      return day.getMonth() + 1 + "/" + day.getDate() + "/" + day.getFullYear();
    }
  },
  props: ["rental"]
};
</script>
<style scoped>
.thumbnail {
  width: 50;
}
td {
  text-align: left;
}
.label-text {
  color: #000;
}
</style>
