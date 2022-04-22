<template>
  <div class="about">
    <Navbar />
    <div class="container">
      <div class="row">
        <div class="col text-center">
          <img src="../assets/img/order.png" width="300" alt="" />
          <h4 class="mt-2">
            Pesanan Anda sedang diproses. <br />Selamat menunggu ya.
          </h4>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Navbar from "@/components/Navbar.vue";

export default {
  name: "StatusView",
  components: {
    Navbar,
  },
};
</script>
