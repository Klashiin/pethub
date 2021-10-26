<template>
  <div class="cadastro">
    <h1>Cadastre Seu Pet</h1>
    <CadastroPet />
  </div>
</template>

<script>
import CadastroPet from "@/components/CadastroPet.vue";

export default {
  name: "Cadastro",
  components: {
    CadastroPet,
  },
};
</script>

<style scoped>
.cadastro {
  text-align: center;
  margin: 0 auto;
  padding: 50px;
}
</style>