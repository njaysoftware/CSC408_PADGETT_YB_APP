<template>
  <page>
    <ActionBar :title="MovieTitle" >
      <NavigationButton text="Back" android.systemIcon="ic_menu_back" @tap="goBack"/>
    </ActionBar>
    <GridLayout rows="*, *, *, *," columns>
      <ListView for="rentor in rentors" >
        <v-template>
          <FlexboxLayout flexdirection="column">
            <GridLayout rows="auto, auto" columns="*, *">
              <Label :text="'Name: ' + rentor.name" row="0" col="0" textWrap="true"/>
              <Label :text="'Email: ' + rentor.email" row="1" col="0" textWrap="true"/>
              <Label :text="'rented: ' + rented(rentor)" row="0" col="1" textWrap="true"/>
              <Label :text="'returned: ' + returned(rentor)" row="1" col="1" textWrap="true"/>
            </GridLayout>
          </FlexboxLayout>
        </v-template>
      </ListView>
    </GridLayout>
  </page>
</template>
<script>
import axios from "axios";
function Rentor({
  id,
  name,
  email,
  email_varified_at,
  isAdmin,
  created_at,
  updated_at,
  pivot
}) {
  this.id = id;
  this.name = name;
  this.email = email;
  this.email_varified_at = email_varified_at;
  this.isAdmin = isAdmin;
  this.created_at = created_at;
  this.updated_at = updated_at;
  this.pivot = pivot;
}
export default {
  data() {
    return {
      MovieId: this.id,
      rentors: [],
      MovieTitle: this.movieTitle
    };
  },
  methods: {
    getRentees() {
      let url ="https://nathanielpadgett.info/api/movies/" + this.MovieId + "/rentals";
      axios.get(url).then(result => {
        result.data[0].rentors.forEach(rentors => {
          this.rentors.push(new Rentor(rentors));
        });
      });
    },
    rented(rent){
      var options = { year: "numeric", month: "numeric", day: "numeric" };
      var day = new Date(rent.pivot.rent_date);
      return day.getMonth() + 1 + "/" + day.getDate() + "/" + day.getFullYear();
    },
    returned(rent){
      var options = { year: "numeric", month: "numeric", day: "numeric" };
      var day = new Date(rent.pivot.rent_date);
      return day.getMonth() + 1 + "/" + day.getDate() + "/" + day.getFullYear();
    },
    goBack() {
      this.$navigateBack();
    }
  },
  mounted() {
    this.getRentees();
    console.log(this.movieTitle)
  },
  props: {
    id: Number,
    movieTitle: String
  }
};
</script>
<style scoped>
ActionBar {
  background-color: rgb(70, 67, 64);
  color: white;
}
GridLayout {
  margin: 10
}
Label {
  font-size: 15;
  color: black;
  
}
page {
  background-color: rgb(224, 224, 224);
}
ListView {
  background-color: rgb(224, 224, 224);
}
</style>
