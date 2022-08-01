<template>
  <div id="main-banner">
  </div>
</template>
<script>
export default {
  name: "Banner",
};
</script>

<style scoped>
#main-banner {
  background-image: url("/public/img/cupcake.png");
  background-position: 0 -130px;
  background-size: cover;
  height: 500px;
  display: flex;
  align-items: center;
  justify-content: flex-start;
 
}
#main-banner h1{
    position: absolute;
    color: black;
    text-align: center;
    font-size:15px ;
    bottom: 130px;
}
</style>