<template>
  <div class="home">
    <h1>PetHub</h1>
    <Cadastro />
  </div>
</template>

<script>
import Cadastro from '@/components/Cadastro.vue'

export default {
  name: 'Home',
  components: {
    Cadastro
  }
}
</script>
