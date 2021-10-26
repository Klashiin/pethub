<template>
  <form id="main-form" @submit.prevent="postToPets">
    <div class="form-row">
      <div class="col-2">
        <label for="nome">Nome:</label>
        <input required type="text" class="form-control" v-model="nome" name="nome" placeholder="Nome" />
      </div>
      <div class="col-2">
        <label for="especie">Espécie:</label>
        <select required v-model="especie" id="especie" name="especie" class="custom-select">
          <option v-for="especie in especies" :key="especie.id" :value="especie.tipo">{{especie.tipo}}</option>
        </select>
      </div>
    </div>
    <div class="form-row">
      <div class="col-2">
        <label for="sexo">Sexo:</label>
        <select required id="sexo" class="custom-select" name="sexo" v-model="sexo">
          <option v-for="sexo in sexos" :key="sexo.id" :value="sexo.tipo">{{sexo.tipo}}</option>
        </select>
      </div>
      <div class="col-2">
        <label for="idade">Idade:</label>
        <select required id="idade" class="custom-select" name="idade" v-model="idade">
          <option v-for="idade in idades" :key="idade.id" :value="idade.tipo">{{idade.tipo}}</option>
        </select>
      </div>
    </div>
    <div class="form-row">
      <div class="col-2">
        <label required for="dono">Nome do dono:</label>
        <input v-model="dono" type="text" class="form-control" id="dono" placeholder="Nome do dono" name="dono" />
      </div>
      <div class="col-2">
        <label for="raça">Raça:</label>
        <input v-model="raca" type="text" class="form-control" id="raca" placeholder="Raça do seu pet" name="raca" />
      </div>
    </div>
    <div class="form-row">
            <div class="col-1">
        <div class="form-check form-check-inline">
          <input v-model="castrado" class="form-check-input" type="checkbox" name="castrado" value="true" id="castrado" />
          <label for="castrado">Castrado</label>
        </div>
      </div>
      <div class="col-1">
        <div class="form-check form-check-inline">
          <input v-model="vacinado" class="form-check-input" type="checkbox" name="vacinado" value="true" id="vacinado" />
          <label for="vacinado">Vacinado</label>
        </div>
      </div>
      <div class="col-1">
        <div v-show="sexo==='F'" class="form-check form-check-inline">
          <input v-model="gravida" class="form-check-input" type="checkbox" id="gravida" name="gravida" value="true" />
          <label for="gravida">Grávida</label>
        </div>
      </div>
    </div>
    <div class="form-row">
      <button type="submit" class="btn btn-primary">Enviar</button>    
    </div>
  </form>
</template>

<script>
import axios from 'axios';

export default {
  name: 'CadastroPet',
  data () {
    return {
      especies: [],
      sexos: [],
      idades: [],
      nome: null,
      especie: null,
      sexo: null,
      idade: null,
      raca: null,
      castrado: null,
      vacinado: null,
      gravida: null,
      dono: null,
    }
  },
  methods: {
    async getInfos() {
      try {
        const res = await axios.get('http://localhost:3000/infos')
        this.especies = res.data.especies
        this.idades = res.data.idades
        this.sexos = res.data.sexos
      } catch (e) {
        console.log(e)
      }
    },
    async postToPets() {
      const res = await axios.post('http://localhost:3000/pets', {
        nome: this.nome,
        especie: this.especie,
        sexo: this.sexo,
        idade: this.idade,
        castrado: this.castrado,
        vacinado: this.vacinado,
        gravida: this.gravida,
        raca: this.raca,
        dono: this.dono
      });      

      console.log(res);

      this.nome = null;
      this.especie = null;
      this.sexo = null;
      this.idade = null;
      this.castrado = null;
      this.vacinado = null;
      this.gravida = null;
      this.raca = null;
      this.dono = null;
    }
  },
  async created () {
    this.getInfos()
  }
}
</script>

<style scoped>
#main-form {
  margin: 10px;
  border-left: 2px solid #5E239D;
}
button {
  margin: 10px;
  background-color: #5E239D;
  border: 2px #5E239D solid;
  font-weight: bold;
}
button:hover {
  background-color: transparent;
  color: #5E239D;
  border: 2px #5E239D solid;
}
.form-row {
  margin: 10px 0px 10px 0px;
}
</style>
