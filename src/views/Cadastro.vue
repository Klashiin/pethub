<template>
    <div class="cadastro">
        <h1>Cadastre Seu Pet</h1>
        <CadastroPet />
    </div>
</template>

<script>
import CadastroPet from '@/components/CadastroPet.vue'

export default ({
    name: "Cadastro",
    components: {
        CadastroPet
    }
})
</script>
