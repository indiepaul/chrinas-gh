<template>
  <footer class="footer">
    <div class="container cols">
      <div class="sub">
        <h3>ADDRESS</h3>
        <br>47/1/172
        <br>Area 47 Sector 1
        <br>Lilongwe, Malawi
      </div>
      <div class="sub">
        <h3>CONTACT</h3>
        <br>Email: info@chrinas.com
        <br>Tel: +265 886 585 999
        <br>
      </div>
      <div class="sub"></div>
    </div>
    <hr>
    <div class="container">
      <span v-html="settings.footer"/>
    </div>
  </footer>
</template>

<script>
export default {
  data() {
    return {
      settings: require("../../data/theme.json"),
      payments: require("../../data/payments.json")
    };
  }
};
</script>

<style scoped>
.footer {
  font-size: 0.8rem;
  padding: 1rem 0 1rem 0;
}
.cols {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-gap: 10px;
}
.sub h3 {
  margin-bottom: 0;
}
@media (max-width: 644px) {
  .cols {
    display: block;
  }
  .sub {
    padding: 10px;
  }
}
</style>
