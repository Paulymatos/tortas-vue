<template>
     <div id="nav">
        <router-link to="/" id="logo-url">
            <img :src="logo" :alt="alt" id="logo">
        </router-link>
    <router-link to="/">Home</router-link> 
    <router-link to="/pedidos">Pedidos</router-link>
  </div>
</template>
<script>
export default {
    name:"Navbar",
    props:["logo","alt"]
}
</script>
<style scoped>
#nav{
  background-color: #f45b8e;
   padding: 15px 50px ;
   display: flex;
   justify-content: flex-end;
   align-items: center;
   font-weight: bold
}
#nav #logo-url{
    margin: auto;
    margin-left: 0;

}
#logo{
    width: 40px;
    height: 40px;
}
#nav a{
    color: #ffafcc;
    text-decoration: none;
    margin: 12px;

}
#nav a:hover{
   color: #bde0fe; 
}
</style>