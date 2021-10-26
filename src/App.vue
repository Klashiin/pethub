<template>
  <div id="header">
    <a href="/"><img src="assets/cat.png" alt="cat logo" /></a>
    <router-link to="/">PetHub</router-link>
    <router-link to="/meus-pets">Meus Pets</router-link>
    <router-link to="/cadastro">Cadastre Seu Pet</router-link>
  </div>
  <div id="content">
    <router-view />
  </div>
  <Footer />
</template>

<script>
import Footer from "./components/Footer.vue";
export default {
  components: {
    Footer,
  },
};
</script>

<style>
* {
  padding: 0px;
  margin: 0px;
  text-align: left;
  font-family: Helvetica, Arial;
  box-sizing: border-box;
}

a {
  text-decoration: none;
  color: white;
  margin: 10px;
  transition: 0.5s;
}

a:hover {
  text-decoration: none;
  color: #CD4631;
}

#footer {
  margin: 0;
  padding: 10px;
  text-align: center;
  background-color: #323031;
  color: white;
}

#content {
  min-height: 500px;;
}

#header {
  background-color: #323031;
  height: 60px;
  font-weight: bold;
  padding: 20px;
}

img {
  width: 30px;
}
</style>
