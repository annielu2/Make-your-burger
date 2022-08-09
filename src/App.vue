<template>
  <NavbarComponent :logo="logo_src" :alt="app_name"/>
  <router-view/>
  <FooterComponent/>
</template>

<script>
import NavbarComponent from "./components/Navbar.vue";
import FooterComponent from "./components/Footer.vue";

export default {
  components: {
    NavbarComponent,
    FooterComponent
  },
  data(){
    return{
      logo_src: "/img/logo.png",
      app_name: "Make your burger"
    }
  }
}
</script>

<style>
  *{
    padding: 0;
    margin: 0;
    box-sizing: border-box;
    font-family: Arial, Helvetica, sans-serif;

  }

  .main-container{
    margin: 50px;
    min-height: 250px;
  }

  h1{
    text-align: center;
    font-size: 42px;
    color: #222;
    bottom: 30px;
    margin: 50px;
  }
</style>
