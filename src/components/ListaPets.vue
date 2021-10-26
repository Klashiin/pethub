<template>
  <div :id="showEdit ? 'show' : 'dontshow'" class="edit">
    <div class="edit-content">
      <span @click="showEdit=false" class="close">&times;</span>
      <form id="main-form" @submit.prevent="editPet(id)">
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
    </div>
  </div>
  <div :id="showModal ? 'show' : 'dontshow'" class="modal">
      <span @click="showModal=false" class="close">&times;</span>
      <p>Pet removido.</p>
  </div>
  <div v-for="pet in pets" :key="pet.id" class="card" style="width: 12rem">
    <img
      class="card-img-top"
      :src="`assets/${pet.especie.toLowerCase()}.jpg`"
      :alt="pet.especie + pet.raca"
    />
    <div @click="deletePet(pet.id)" class="close">&times;</div>
    <button @click="toggleEdit($event), getPetData(pet.id)" class="btn btn-primary btn-small btnq">EDITAR</button>
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
      id: null,
      pets: [],
      showModal: false,
      showEdit: false,
      sexos: [],
      idades: [],
      esoecies: [],
      nome: null,
      especie: null,
      sexo: null,
      idade: null,
      raca: null,
      castrado: null,
      vacinado: null,
      gravida: null,
      dono: null
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
    async getInfos() {
      try {
        const res = await axios.get('http://localhost:3000/infos');
        this.sexos = res.data.sexos;
        this.idades = res.data.idades;
        this.especies = res.data.especies;
      } catch (e) {
        console.log(e)
      }
    },
    async deletePet(id) {
      const res = await axios.delete(`http://localhost:3000/pets/${id}`);
      console.log(res);
      this.getPets();
      this.showModal = !this.showModal;
      setTimeout(() => this.showModal = !this.showModal, 4000);
    },
    toggleEdit() {
      this.showEdit = !this.showEdit;
    },
    async getPetData(id) {
      try {
        const res = await axios.get(`http://localhost:3000/pets/${id}`)
        this.id = id;
        this.nome = res.data.nome;
        this.especie = res.data.especie;
        this.sexo = res.data.sexo;
        this.idade = res.data.idade;
        this.vacinado = res.data.vacinado;
        this.castrado = res.data.castrado;
        this.gravida = res.data.gravida;
        this.raca = res.data.raca;
        this.dono = res.data.dono;
      } catch (e) {
        console.log(e)
      }
    },
    async editPet(id) {
      const res = await axios.patch(`http://localhost:3000/pets/${id}`, {
        nome: this.nome,
        especie: this.especie,
        sexo: this.sexo,
        idade: this.idade,
        castrado: this.castrado,
        vacinado: this.vacinado,
        gravida: this.gravida,
        raca: this.raca,
        dono: this.dono
      })
      this.nome = null;
      this.especie = null;
      this.sexo = null;
      this.idade = null;
      this.castrado = null;
      this.vacinado = null;
      this.gravida = null;
      this.raca = null;
      this.dono = null;
      this.id = null;

      this.toggleEdit();
      this.getPets();

      console.log(res)
    }
  },
  async created() {
    this.getPets();
    this.getInfos();
  },
};
</script>

<style scoped>
.card {
  float: left;
  margin: 10px;
  height: 380px;
  position: relative;
}
.card-img-top {
  display: block;
  height: 200px;
  object-fit: cover;
}
.close {
  position: absolute;
  top: 8px;
  right: 16px;
  font-weight: bold;
  color: red;
}
.close:hover,
.close:focus {
  cursor: pointer;
}
.modal {
  position: fixed;
  width: 300px;
  height: 100px;
  top: -30%;
  margin-left: auto;
  margin-right: auto;
  left: 0;
  right: 0;
  z-index: 1;
  background-color: #323031;
  margin: 15% auto;
  padding: 20px;
  border: 1px solid #888;
  color: white;
  font-weight: bold;
}
#show {
  display: block;
}
#dontshow {
  display: none;
}
.btnq {
  padding: 0;
  position: absolute;
  top: 8px;
  left: 16px;
  font-weight: bold;
  font-size: 10px;
  width: 50px;
  height: 30px;
}
.edit {
  position: fixed;
  z-index: 1;
  width: 100%;
  height: 100%;
  left: 0;
  top: 0;
  overflow: auto;
  background-color: rgb(0,0,0);
  background-color: rgba(0,0,0,0.4);
}
.edit-content {
  position: fixed;
  background-color: #fff;
  margin: 15% auto;
  color: black;
  font-weight: bold;
  padding: 20px;
  margin-left: auto;
  margin-right: auto;
  left: 0;
  right: 0;
}
</style>
