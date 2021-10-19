<template>
  <div id="nav">
    <router-link to="/">Home</router-link> |
    <router-link to="/meus-pets">Meus Pets</router-link> |
    <router-link to="/cadastro">Cadastre Seu Pet</router-link> 
  </div>
  <router-view/>
</template>

<style>
* {
  padding: 0px;
  margin: 0px;
  text-align: left;
  font-family: Helvetica, Arial;
}

a {
  text-decoration: none;
}
</style>
