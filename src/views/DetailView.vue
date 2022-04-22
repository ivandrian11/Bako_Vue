<template>
  <div class="detail">
    <Navbar />

    <div class="container mt-3">
      <!-- breadcrumb -->
      <div class="row">
        <div class="col">
          <nav aria-label="breadcrumb">
            <ol class="breadcrumb">
              <li class="breadcrumb-item">
                <router-link class="text-dark" to="/"> Home </router-link>
              </li>
              <li class="breadcrumb-item">
                <router-link class="text-dark" to="/product">
                  Baju
                </router-link>
              </li>
              <li class="breadcrumb-item active" aria-current="page">
                {{ product.nama }}
              </li>
            </ol>
          </nav>
        </div>
      </div>

      <!-- content -->
      <div class="row">
        <div class="col-md-6">
          <img
            :src="'../assets/img/' + product.gambar"
            class="img-fluid shadow"
          />
        </div>
        <div class="col-md-6">
          <h2>
            <strong>{{ product.nama }}</strong>
          </h2>
          <hr />
          <h4>Harga: {{ product.harga }}</h4>
          <form class="mt-4" v-on:submit.prevent>
            <div class="form-group">
              <label for="jumlah">Jumlah Pesan: </label>
              <input
                type="number"
                class="form-control"
                v-model="order.jumlah"
              />
            </div>
            <div class="form-group">
              <label for="keterangan">Catatan :</label>
              <textarea
                class="form-control"
                placeholder="Isi catatan disini (jika ada)"
                v-model="order.catatan"
              />
            </div>
            <button type="submit" @click="addToCart" class="btn btn-success">
              <b-icon-cart></b-icon-cart> Tambahkan Keranjang
            </button>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Navbar from "@/components/Navbar.vue";
import axios from "axios";

export default {
  name: "DetailView",
  components: {
    Navbar,
  },
  data() {
    return {
      product: {},
      order: {},
    };
  },
  methods: {
    setData(data) {
      this.product = data;
    },
    addToCart() {
      if (!this.order.jumlah) {
        this.$toast.error("Field jumlah tidak boleh kosong!", {
          position: "top-right",
        });
      } else {
        this.order.product = this.product;
        axios
          .post(
            "https://my-json-server.typicode.com/ivandrian11/fake-api/cart",
            this.order
          )
          .then(() => {
            this.$router.push({ path: "/cart" });
            this.$toast.success("Pesanan masuk ke keranjang.", {
              position: "top-right",
            });
          })
          .catch((error) => console.log(error));
      }
    },
  },

  mounted() {
    axios
      .get(
        "https://my-json-server.typicode.com/ivandrian11/fake-api/products/" +
          this.$route.params.id
      )
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