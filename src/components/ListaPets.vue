<template>
  <div v-for="pet in pets" :key="pet.id" class="card" style="width: 18rem">
    <img
      class="card-img-top"
      :src="`assets/${pet.especie.toLowerCase()}.jpg`"
      :alt="pet.especie + pet.raca"
    />
    <div class="card-body">
      <h5 class="card-title">{{ pet.nome }}</h5>
      <p class="card-text">
        {{ pet.sexo }} | {{ pet.idade }} |
        {{ pet.castrado ? "Castrado" : "Não-castrado" }} |
        {{ pet.vacinado ? "Vacinado" : "Não-vacinado" }} 
        {{ pet.gravida ? "| Grávida" : null }}
        {{ pet.raca != null ? `| ${pet.raca}` : null }}
      </p>
      <small>Tutor: {{ pet.dono }}</small>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "ListaPets",
  data() {
    return {
      pets: [],
    };
  },
  methods: {
    async getPets() {
      try {
        const res = await axios.get("http://localhost:3000/pets");
        this.pets = res.data;
      } catch (e) {
        console.log(e);
      }
    },
  },
  async created() {
    this.getPets();
  },
};
</script>

<style scoped>
.card {
  float: left;
  margin: 10px;
  min-height: 380px;
}
.card-img-top {
  display: block;
  height: 200px;
  object-fit: cover;
}
</style>
