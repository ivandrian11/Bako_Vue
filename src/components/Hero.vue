<template>
  <div class="container">
    <div class="d-none d-md-block">
      <div class="row align-items-center">
        <div class="col-md justify-content-center">
          <h2>
            <strong> Kamu bisa membeli baju koko </strong>
            cuma dari rumah aja.
          </h2>
          <p>Karena kami siap mengantar ke rumah kamu.</p>
          <router-link to="/product" class="btn btn-lg btn-success">
            <b-icon-arrow-right></b-icon-arrow-right> Pesan
          </router-link>
        </div>
        <div class="col-md">
          <img src="../assets/img/hero.png" width="100%" alt="" />
        </div>
      </div>
    </div>

    <div class="d-sm-block d-md-none">
      <div class="row align-items-center">
        <div class="col-md mb-3">
          <img src="../assets/img/hero.png" width="100%" alt="" />
        </div>
        <div class="col-md justify-content-center">
          <h2>
            <strong> Kamu bisa membeli baju koko </strong>
            cuma dari rumah aja.
          </h2>
          <p>Karena kami siap mengantar ke rumah kamu.</p>
          <router-link to="/product" class="btn btn-lg btn-success">
            <b-icon-arrow-right></b-icon-arrow-right> Pesan
          </router-link>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "HeroIllustration",
};
</script>

<style>
</style>