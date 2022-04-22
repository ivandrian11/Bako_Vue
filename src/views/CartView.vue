<template>
  <div class="keranjang">
    <Navbar :updateData="products" />

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
                Keranjang
              </li>
            </ol>
          </nav>
        </div>
      </div>

      <!-- Table -->
      <div class="row mt-2">
        <div class="col">
          <h2>Keranjang <strong>Saya</strong></h2>
          <div class="table-responsive mt-4">
            <table class="table">
              <thead>
                <tr>
                  <th scope="col">#</th>
                  <th scope="col">Gambar</th>
                  <th scope="col">Nama</th>
                  <th scope="col">Catatan</th>
                  <th scope="col">Harga</th>
                  <th scope="col">Jumlah</th>
                  <th scope="col">Total Harga</th>
                  <th class="text-center" scope="col">Aksi</th>
                </tr>
              </thead>
              <tbody>
                <tr v-for="(product, i) in products" :key="product.id">
                  <th>{{ i + 1 }}</th>
                  <td>
                    <img
                      :src="'../assets/img/' + product.product.gambar"
                      class="img-fluid shadow"
                      width="100"
                    />
                  </td>
                  <th>{{ product.product.nama }}</th>
                  <td>{{ product.catatan ? product.catatan : "-" }}</td>
                  <td>Rp{{ product.product.harga }}</td>
                  <td>{{ product.jumlah }}</td>
                  <th>Rp{{ product.jumlah * product.product.harga }}</th>
                  <td align="center" class="text-danger">
                    <b-icon-trash
                      @click="deleteData(product.id)"
                    ></b-icon-trash>
                  </td>
                </tr>
                <tr>
                  <td colspan="6" align="right">
                    <strong>Total Keseluruhan :</strong>
                  </td>
                  <th>Rp{{ products ? calculateTotalPrice : 0 }}</th>
                  <td></td>
                </tr>
              </tbody>
            </table>
          </div>
        </div>
      </div>

      <!-- Form -->
      <div class="row justify-content-end">
        <div class="col-md-4">
          <form class="mt-4" v-on:submit.prevent>
            <div class="form-group">
              <label for="nama">Nama:</label>
              <input type="text" class="form-control" v-model="order.nama" />
            </div>
            <div class="form-group">
              <label for="alamat">Alamat</label>
              <textarea
                class="form-control"
                placeholder="Isi alamat kamu disini"
                v-model="order.alamat"
              />
            </div>
            <button
              @click="checkout"
              type="submit"
              class="btn btn-success float-right"
            >
              <b-icon-cart></b-icon-cart> Checkout
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
  name: "CartView",
  components: {
    Navbar,
  },
  data() {
    return {
      products: [],
      order: {},
    };
  },
  methods: {
    setData(data) {
      this.products = data;
    },
    deleteData(id) {
      // Delete
      axios
        .delete(
          "https://my-json-server.typicode.com/ivandrian11/fake-api/cart/" + id
        )
        .then(() => {
          this.$toast.warning("Pesanan berhasil dihapus.", {
            position: "top-right",
          });
          // Reload
          axios
            .get(
              "https://my-json-server.typicode.com/ivandrian11/fake-api/cart"
            )
            .then((response) => this.setData(response.data))
            .catch(function (error) {
              // handle error
              console.log(error);
            });
        })
        .catch(function (error) {
          // handle error
          console.log(error);
        });
    },
    checkout() {
      if (this.products.length == 0) {
        this.$toast.error("Kamu belum menambahkan barang.", {
          position: "top-right",
        });
      } else {
        if (!this.order.nama || !this.order.alamat) {
          this.$toast.error("Field nama dan alamat tidak boleh kosong!", {
            position: "top-right",
          });
        } else {
          this.order.products = this.products;

          this.products.map((item) =>
            axios
              .delete(
                "https://my-json-server.typicode.com/ivandrian11/fake-api/cart/" +
                  item.id
              )
              .catch(function (error) {
                // handle error
                console.log(error);
              })
          );

          axios
            .post(
              "https://my-json-server.typicode.com/ivandrian11/fake-api/order",
              this.order
            )
            .then(() => {
              this.$router.push({ path: "/status" });
              this.$toast.success("Barang berhasil dipesan.", {
                position: "top-right",
              });
            })
            .catch((error) => console.log(error));
        }
      }
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
  computed: {
    calculateTotalPrice() {
      return this.products.reduce(
        (items, data) => items + data.product.harga * data.jumlah,
        0
      );
    },
  },
};
</script>

<style>
</style>