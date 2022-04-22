<template>
  <div class="home">
    <Navbar />
    <Hero />

    <div class="container">
      <div class="row mt-5">
        <div class="col-md">
          <h2>Baju Koko <strong>Terbaik</strong></h2>
        </div>
        <div class="col-md">
          <router-link to="/product" class="btn btn-success float-right">
            <b-icon icon="arrow-right-square"></b-icon> Lihat Semua
          </router-link>
        </div>
      </div>

      <div class="row mb-4">
        <div
          class="col-md-4 mt-4"
          v-for="product in products"
          :key="product.id"
        >
          <CardProduct :product="product" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import Hero from "@/components/Hero.vue";
import Navbar from "@/components/Navbar.vue";
import CardProduct from "@/components/CardProduct.vue";
import axios from "axios";

export default {
  name: "HomeView",
  components: {
    Navbar,
    Hero,
    CardProduct,
  },
  data() {
    return {
      products: [],
    };
  },
  methods: {
    setData(data) {
      this.products = data;
    },
  },
  mounted() {
    axios
      .get(
        "https://my-json-server.typicode.com/ivandrian11/fake-api/best-products"
      )
      .then((response) => this.setData(response.data))
      .catch(function (error) {
        // handle error
        console.log(error);
      });
  },
};
</script>
