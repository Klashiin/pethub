<template>
  <div class="home">
    <div class="banner">
      <h1>PetHub</h1>
      <h2>Atendimento 24h/7 para o seu bichinho.</h2>
      <h2>Tratamento incluso com os melhores veterinários.</h2>
      <h2>Conecte-se à nossa rede de profissionais.</h2>
    </div>
  </div>
</template>

<script>
export default {
  name: "Home",
};
</script>

<style scoped>
.home {
  position: relative;
}

.banner {
  background-image: url("/assets/banner.jpg");
  background-size: cover;
  height: 500px;
  padding: 10px;
}

.banner h1 {
  margin: 10px;
  padding: 10px;
  font-size: 60px;
  font-weight: bold;
  color: white;
  border-left: 8px solid #cd4631;
}

.banner h2 {
  margin: 10px;
  padding: 10px;
  color: white;
  font-weight: bold;
  border-left: 4px solid #cd4631;
}
</style>
