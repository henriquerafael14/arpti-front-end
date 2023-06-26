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
  data () {
    return {
      programas: _PROGRAMAS
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
