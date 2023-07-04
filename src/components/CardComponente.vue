<template>
  <div class="card flex align-items-center justify-content-center">
    <Card >
        <template #header>
          <!-- <img :src="programa.imagem" alt="Imagem do Programa" /> -->
        </template>
        <template #title>{{ programa.nome }}</template>
        <template #subtitle>{{ programa.subtitulo }}</template>
        <template #content>
            <p>
                {{ programa.descricao }}
            </p>
        </template>
        <template #footer>
            <Button v-if="programa.nome == 'Arpti'" label="Baixar" @click="baixarInstalador"/>
            <Button v-if="programa.nome != 'Arpti'" label="Instalar" severity="secondary" style="margin-left: 0.5em"  @click="obterInstalacao"/>
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

    baixarInstalador () {
      window.open(this.programa.link, '_blank')
    },

    obterInstalacao () {
      this.carregando = true
      axios.get('https://localhost:44348/api/Robo' + this.programa.endpoint)
        .then(response => {
          console.log('response', response)
        })
        .catch(error => {
          console.log('error', error.message)
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
