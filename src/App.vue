<template>
  <CabecalhoComponente/>
  <div class="grid-container">
    <CardComponente v-for="programa in programas" :key="programa.id" :programa="programa" class="grid-item"/>
  </div>
</template>

<script>
import CardComponente from './components/CardComponente.vue'
import CabecalhoComponente from './components/CabecalhoComponente.vue'
import _PROGRAMAS from './Programas.json'
export default {
  components: {
    CabecalhoComponente,
    CardComponente
  },

  methods: {
    obterImagens () {
      const imagens = ['../assets/ARP.png', '../assets/winrar.jpg', '../assets/operagx.jpg', '', '', '', '', '', '']
      const programas = _PROGRAMAS
      if (programas.length === imagens.length) {
        programas.forEach((programa, indice) => {
          const imagem = imagens[indice]
          programa.imagem = imagem
        })
      }

      return programas
    }
  },

  data () {
    const programasComImagens = this.obterImagens()
    return {
      programas: programasComImagens
    }
  }
}
</script>

<style>
.grid-container {
  margin-top: 100px;
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-template-rows: repeat(3, 1fr);
  gap: 20px;
}

</style>
