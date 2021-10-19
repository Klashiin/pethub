<template>
  <form id="sub-form">
  </form>
  <form id="main-form">
    <div class="form-row">
      <div class="col-2">
        <label for="nome">Nome:</label>
        <input type="text" class="form-control" v-model="nome" name="nome" placeholder="Nome" />
      </div>
      <div class="col-2">
        <label for="especie">Espécie:</label>
        <select v-model="especie" id="especie" name="especie" class="custom-select">
          <option value="">Selecione a espécie:</option>
          <option value="outros">Outros</option>
        </select>
      </div>
    </div>
    <div v-show="especie==='outros'" class="form-row">
      <div class="col-4">
        <label for="novaespecie">Adicione uma espécie:</label>
        <input v-model="novaespecie" type="text" class="form-control" id="novaespecie" name="novaespecie" placeholder="Adicione uma espécie" form="sub-form" />
      </div>
    </div>
    <div v-show="especie==='outros'" class="form-row">
      <button type="submit" class="btn btn-primary" form="sub-form">Adicionar</button>
    </div>
    <div class="form-row">
      <div class="col-2">
        <label for="sexo">Sexo:</label>
        <select id="sexo" class="custom-select" name="sexo" v-model="sexo">
          <option value="">Selecione o sexo:</option>
        </select>
      </div>
      <div class="col-2">
        <label for="idade">Idade:</label>
        <select id="idade" class="custom-select" name="idade" v-model="idade">
          <option value="">Selecione a idade:</option>
        </select>
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
      <div class="col-2">
        <label for="dono">Nome do dono:</label>
        <input v-model="dono" type="text" class="form-control" id="dono" placeholder="Nome do dono" name="dono" />
      </div>
      <div class="col-2">
        <label for="raça">Raça:</label>
        <select v-model="raca" id="raça" class="custom-select" name="raça">
          <option value="">Selecione a raça:</option>
        </select>
      </div>
    </div>
    <div class="form-row">
      <button type="submit" class="btn btn-primary">Enviar</button>    
    </div>
  </form>
</template>

<script>
export default {
  name: 'CadastroPet',
  data () {
    return {
      especies: null,
      sexos: null,
      idades: null,
      racas: null,
      nome: null,
      especie: null,
      sexo: null,
      idade: null,
      raca: null,
      castrado: null,
      vacinado: null,
      gravida: null,
      dono: null,
      novaespecie: null,
    }
  },
  methods: {
    
  }
}
</script>

<style scoped>
#main-form {
margin: 10px;
}
button {
margin: 10px;
}
.form-row {
margin: 10px 0px 10px 0px;
}
</style>
