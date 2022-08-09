<template>
  <nav>
    <router-link to="/" id="logo-url">
        <img :src="logo" :alt="alt" id="logo">
    </router-link>
    <div class="container">
          <router-link to="/">Home</router-link>
          <router-link to="/about">About</router-link>
          <router-link to="/pedidos">Pedidos</router-link>
    </div>
  </nav>
</template>

<script>
export default{
    name: 'NavbarComponent',
    props: ["logo", "alt"]
}

</script>

<style scoped>
  nav{
    background-color: rgba(0, 0, 0, 0.95);
    padding: 15px 50px;
    display: flex;
    justify-content: flex-end;
    align-items: center;
  }

  #logo-url{
    margin: auto;
    margin-left: 0;

  }

  #logo{
    width: 40px;
    height: 40px;
  }

  nav a{
    overflow: hidden;
    text-decoration: none;
    color: #FCBA03;
    margin: 15px;
    position: relative;

  }


 .container a:after{
    content: "";
    position: absolute;
    bottom: -8px;
    left: 0;
    width: 0;
    height: 2px;
    background-color: #FCBA03;
    border-radius: 8px;
    transition: all 0.3s;
  }

  .container a:hover:after{
    width: 100%;
  }


</style>