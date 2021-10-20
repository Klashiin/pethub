<template>
  <div class='meus-pets'>
    <h1>Meus Pets</h1>
    <ListaPets />
  </div>
</template>

<script>
import ListaPets from '@/components/ListaPets.vue'

  export default {
    name: 'MeusPets',
    components: {
      ListaPets
    }
  }
</script>