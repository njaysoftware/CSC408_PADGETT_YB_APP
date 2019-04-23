<template>
  <Page>
    <ActionBar :title="'Rentals for ' + customer_name" android:flat="true">
      <NavigationButton text="Back" android.systemIcon="ic_menu_back" @tap="goBack"/>
    </ActionBar>
    <ListView for="rental in rentals" class="list-group" style="height:100%">
      <v-template>
        <customer-rental-history :rental="rental"></customer-rental-history>
      </v-template>
    </ListView>
  </Page>
</template>
<script>
import axios from "axios";
import CustomerRentalHistory from "@/components/CustomerComponents/CustomerRentalHistory.vue";
import { error } from "util";
function Rental({ id, title, rating, length, pivot }) {
  this.id = parseInt(pivot.id);
  this.title = title;
  this.rating = rating;
  this.length = length;
  this.transaction = pivot;
}
export default {
  data() {
    return {
      customer_name: "",
      rentals: []
    };
  },
  methods: {
    getRentals() {
      let url =
        "https://nathanielpadgett.info/api/customers/" + this.id + "/rentals";
      axios.get(url).then(({ data }) => {
        this.customer_name = data[0].name;
        data[0].rentals.forEach(rental => {
          this.rentals.push(new Rental(rental));
        });
      }),
        error => {
          console.log(error);
        };
    },
    goBack() {
      this.$navigateBack();
    }
  },
  props: ["id"],
  components: {
    CustomerRentalHistory
  },
  created() {
    this.getRentals();
  }
};
</script>
<style scoped>
ActionBar {
   color: white;
  background-color:rgb(70, 67, 64);
}
ListView {
   background-color: rgb(224, 224, 224);
}
</style>
