<template>
  <div>
    <b-navbar toggleable="lg" type="light">
      <div class="container mb-4">
        <!-- <b-navbar-brand href="#">BaKo</b-navbar-brand> -->

        <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

        <b-collapse id="nav-collapse" is-nav>
          <b-navbar-nav>
            <li class="nav-item">
              <router-link class="nav-link" to="/">Home</router-link>
            </li>
            <li class="nav-item">
              <router-link class="nav-link" to="/product">Baju</router-link>
            </li>
          </b-navbar-nav>

          <!-- Right aligned nav items -->
          <b-navbar-nav class="ml-auto">
            <li class="nav-item">
              <router-link class="nav-link" to="/cart">
                Keranjang
                <b-icon icon="bag-check"></b-icon>
                <b-badge variant="success" class="ml-2">{{
                  updateData ? updateData.length : products.length
                }}</b-badge>
              </router-link>
            </li>
          </b-navbar-nav>
        </b-collapse>
      </div>
    </b-navbar>
  </div>
  <!-- <nav class="navbar navbar-expand-lg navbar-light">
    <div class="container mb-4">
      <a class="navbar-brand" href="#">Bako</a>
      <button
        class="navbar-toggler"
        type="button"
        data-bs-toggle="collapse"
        data-bs-target="#navbarSupportedContent"
        aria-controls="navbarSupportedContent"
        aria-expanded="false"
        aria-label="Toggle navigation"
      >
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarSupportedContent">
        <ul class="navbar-nav mr-auto mb-2 mb-lg-0">
          <li class="nav-item">
            <router-link class="nav-link" to="/">Home</router-link>
          </li>
          <li class="nav-item">
            <router-link class="nav-link" to="/product">Baju</router-link>
          </li>
        </ul>

        <ul class="navbar-nav ml-auto mb-2 mb-lg-0">
          <li class="nav-item">
            <router-link class="nav-link" to="/cart">
              Keranjang
              <b-icon icon="bag-check"></b-icon>
              <b-badge variant="success" class="ml-2">{{
                updateData ? updateData.length : products.length
              }}</b-badge>
            </router-link>
          </li>
        </ul>
      </div>
    </div>
  </nav> -->
</template>

<script>
import axios from "axios";

export default {
  name: "NavBar",
  props: ["updateData"],
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
      .get("https://my-json-server.typicode.com/ivandrian11/fake-api/cart")
      .then((response) => this.setData(response.data))
      .catch(function (error) {
        // handle error
        console.log(error);
      });
  },
};
</script>
