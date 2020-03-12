<template>
  <footer class="footer">
    <div class="container cols">
      <div class="sub">
        ADDRESS
        <br>
        <hr>47/1/172
        <br>Area 47 Sector 1
        <br>Lilongwe, Malawi
      </div>
      <div class="sub">
        CONTACT
        <br>
        <hr>Email: chrinasll@gmail.com
        <br>Tel +44 7912207009
        <br>+265 999 950 095
        <br>
      </div>
      <div class="sub">WE ACCEPT</div>
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
      settings: require("../../data/theme.json")
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
</style>
