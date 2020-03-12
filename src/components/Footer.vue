<template>
  <footer class="footer">
    <div class="container cols">
      <div class="sub">
        ADDRESS
        <br>47/1/172
        <br>Area 47 Sector 1
        <br>Lilongwe, Malawi
      </div>
      <div class="sub">
        CONTACT
        <br>Email: chrinasll@gmail.com
        <br>Tel +44 7912207009
        <br>+265 999 950 095
        <br>
      </div>
      <div class="sub">
        WE ACCEPT
        <div class="cards">
          <img
            v-for="type in payments.payment_types"
            :key="type.name"
            :src="type.image"
            :alt="type.name"
          >
        </div>
      </div>
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
  padding: 6rem 0;
}
.cols {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-gap: 10px;
}
.sub {
  display: grid;
}
.cards {
  display: flex;
}
.cards img {
  height: 30px;
  width: 65px;
  padding: 5px;
}
@media (max-width: 644px) {
  .cards img {
    height: 14px;
    width: 30px;
    padding: 2px;
  }
  .cols {
    display: block;
  }
  .sub {
    padding: 10px;
  }
}
</style>
