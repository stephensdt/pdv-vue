<template>
  <div id="app">
    <div >
      <Componente
      :titulo="tituloSemClasse"
      temSubtitulo
      @trocarTemperatura="mostarTemperatura"
      ref="componenteSemClasse"
      />
      <button @click="$refs.componenteSemClasse.printar('oi')">
        chamar metodo do filho
      </button>
  
      <ComponenteComClasse
      :titulo="tituloComClasse"
      temSubtitulo
      @trocarTemperatura="mostarTemperatura"
      ref="componenteCemClasse"
      />
      <button @click="$refs.componenteComClasse.printar('oi')">
        chamar metodo do filho
      </button>
    </div>
  </div>
</template>

<script>
import Componente from './components/Componente.vue'
import ComponenteComClasse from './components/ComponenteComClasse.vue'
export default {
  components: {
    Componente,
    ComponenteComClasse,
  },
  data() {
    return {
      tituloSemClasse: 'Componente Vue sem Class!!',
      tituloComClasse: 'Componente Vue com Class!!',
    }
  },
  methods: {
    mostarTemperatura(temperatura) {
      console.log('Temperatura: ', temperatura)
    }
  }
}
</script>

<style>
#app {
  display: flex;
}

</style>
