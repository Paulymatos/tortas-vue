<template>
     <div id="nav">
       
    <router-link to="/">Home</router-link> 
     <router-link to="/" id="logo-url">
            <img :src="logo" :alt="alt" id="logo">
        </router-link>
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
  background-color: #ffc4d6 ;
   display:flex;
   justify-content: center;
   align-items: center;
   font-weight: bold;
   gap: 20px;
  
}
/* #nav #logo-url{
    margin: auto;
    margin-left: 0;

} */
#logo{
    width: 40px;
    height: 40px;
}
#nav a{
    
    color: white ;
    text-decoration: none;
    
  
}
#nav a:hover{
   color: #ff7096; 
}
</style>