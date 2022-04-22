<template>
  <div class="baju">
    <Navbar />
    <div class="container">
      <div class="row">
        <div class="col">
          <h2>Daftar <strong>Baju</strong></h2>
        </div>
      </div>

      <div class="row mt-3">
        <div class="col">
          <div class="input-group mb-3">
            <input
              v-model="keyword"
              type="text"
              class="form-control"
              placeholder="Cari Baju Yang Kamu Sukai"
              aria-label="Cari"
              aria-describedby="basic-addon1"
              @keyup="search"
            />
            <span class="input-group-text" id="basic-addon1">
              <b-icon-search></b-icon-search>
            </span>
          </div>
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
import CardProduct from "@/components/CardProduct.vue";
import Navbar from "@/components/Navbar.vue";
import axios from "axios";

export default {
  name: "ProductView",
  components: {
    Navbar,
    CardProduct,
  },
  data() {
    return {
      products: [],
      keyword: "",
    };
  },
  methods: {
    setData(data) {
      this.products = data;
    },
    search() {
      axios
        .get(
          "https://my-json-server.typicode.com/ivandrian11/fake-api/products?q=" +
            this.keyword
        )
        .then((response) => this.setData(response.data))
        .catch(function (error) {
          // handle error
          console.log(error);
        });
    },
  },
  mounted() {
    axios
      .get("https://my-json-server.typicode.com/ivandrian11/fake-api/products")
      .then((response) => this.setData(response.data))
      .catch(function (error) {
        // handle error
        console.log(error);
      });
  },
};
</script>

<style>
</style>