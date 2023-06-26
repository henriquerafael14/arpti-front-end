<template>
  <div class="card flex align-items-center justify-content-center">
    <Card style="width: 25em">
        <template #header>
          <img :src="programa.imagem" alt="Imagem do Item" />
        </template>
        <template #title>{{ programa.nome }}</template>
        <template #subtitle>{{ programa.subtitulo }}</template>
        <template #content>
            <p>
                {{ programa.descricao }}
            </p>
        </template>
        <template #footer>
            <Button label="Baixar" @click="baixarInstalador"/>
            <Button label="Instalar" severity="secondary" style="margin-left: 0.5em"  @click="obterInstalacao"/>
        </template>
      </Card>
      <!-- <ProgressSpinner class="indicador-carregando" strokeWidth="8" fill="var(--surface-ground)" animationDuration=".5s" aria-label="Custom ProgressSpinner" v-if="carregando"/> -->
</div>
</template>

<script>
import axios from 'axios'
import Card from 'primevue/card'
import Button from 'primevue/button'
// import ProgressSpinner from 'primevue/progressspinner'
export default {
  props: {
    programa: {
      type: Object,
      required: true
    }
  },
  components: {
    Card,
    Button
    // ProgressSpinner
  },
  methods: {
    alertFunc () {
      alert('instalar!')
    },

    baixarInstalador () {
      alert('Baixar Instalador')
    },

    obterInstalacao () {
      const apiUrl = 'https://localhost:44348​/api​/Robo​/instalacao-winrar'
      this.carregando = true
      axios.get(apiUrl)
        .then(response => {
          console.log('response', response)
        })
        .catch(error => {
          console.log('error', error)
          setTimeout(this.alertFunc, 3000)
        })
        .finally(() => {
          this.carregando = false
        })
    }
  },
  data () {
    return {
      carregando: true
    }
  }
}
</script>

<style>
.indicador-carregando {
  position: fixed;
  width: 50px;
  height: 50px;
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
  background-color: rgba(250, 250, 250, 0.5);
  z-index: 9999;
}
</style>
