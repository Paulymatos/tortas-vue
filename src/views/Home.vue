<template>
  <Banner/> 
  <div class="main-container">
    <h1>Monte seu Cupcake :</h1>
    <CupForm/>
  </div>
</template>

<script>
import CupForm from "../components/CupForm.vue"
import Banner from "../components/Banner.vue"
export default {
  name: "Home",
  components: {
    Banner,
    CupForm
  }
};
</script>
<style scoped>
.main-container h1{
color: #ffb7c3;
}
</style>