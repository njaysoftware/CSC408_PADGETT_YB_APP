<template>
  <Page>
    <ActionBar>
      <StackLayout orientation="horizontal">
        <Image src="res://icon" width="40" height="40" verticalAlignment="center"/>
        <Label text=" Yellow Bucket" fontSize="24" verticalAlignment="center"/>
      </StackLayout>
    </ActionBar>
    <TabView
      android:tabBackgroundColor="#726c69"
      android:tabTextColor="#d6cfcb"
      android:selectedTabTextColor="#ffffff"
      androidSelectedTabHighlightColor="#ffffff"
    >
      <TabViewItem title="Movies">
        <movie-component v-bind:movies="this.movies"></movie-component>
      </TabViewItem>
      <TabViewItem title="Customers">
        <customer-component :customers="customers"></customer-component>
      </TabViewItem>
      <TabViewItem title="About">
        <GridLayout columns="*" rows="*" >          
          <Label class="message" :text="aboutMsg" col="0" row="0" textWrap="true"/>
        </GridLayout>
      </TabViewItem>
    </TabView>
  </Page>
</template>
<script >
function Movie({
  id,
  title,
  rating,
  length,
  description,
  onDVD,
  onBluRay,
  deleted_at,
  created_at,
  updated_at
}) {
  this.id = id;
  this.title = title;
  this.rating = rating;
  this.length = length;
  this.description = description;
  this.onDVD = onDVD;
  this.onBluRay = onBluRay;
  this.deleted_at = deleted_at;
  this.created_at = created_at;
  this.updated_at = updated_at;
}
function Customer({ id, name, email, isAdmin }) {
  this.id = id;
  this.name = name;
  this.email = email;
  this.isAdmin = isAdmin;
}

import MovieComponent from "@/components/MovieComponents/MovieComponent.vue";
import CustomerComponent from "@/components/CustomerComponents/CustomerComponent.vue";
import axios from "axios";
export default {
  data() {
    return {
      movies: [],
      customers: [],
      aboutMsg: "Welcome to Yellow Bucket. We are a movies rentals business that you can rent both hidef and standard movies from. You can rent the product and then pay us for it. Please enjoy your visit and take your time as you browse our large collection of movies"
    };
  },
  methods: {
    getMovieData() {
      let url = "https://nathanielpadgett.info/api/movies";
      axios.get(url).then(results => {
        results.data.forEach(movie => {
          this.movies.push(new Movie(movie));
        });
      });
    },
    getCustomerData() {
      axios.get("https://nathanielpadgett.info/api/customers").then(
        result => {
          result.data.forEach(customer => {
            this.customers.push(new Customer(customer));
          });
        },
        error => {
          console.error(error);
        }
      );
    }
  },
  mounted() {
    this.getMovieData();
    this.getCustomerData();
  },
  components: {
    MovieComponent,
    CustomerComponent
  }
};
</script>

<style scoped>
ActionBar {
  background-color: rgb(70, 67, 64);
  color: #ffffff;
  text-align: center;
}
.action-bar {
  vertical-align: center;
}
.message {
  vertical-align: center;
  text-align: center;
  font-size: 20;
  color: #333333;
}
Page {
  background-color: #ffffff;
}
GridLayout {
  background-color: rgb(224,224, 224)
}
</style>
