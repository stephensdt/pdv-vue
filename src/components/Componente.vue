<template>
    <div>
        <h3>{{ titulo }}</h3>
        <h4 v-if="temSubtitulo">{{ subtitulo }}</h4>
        <div> {{ mensagem }} </div>
        <div>
            <input v-model="mensagem" @blur="perdeuFoco">
            <button v-on:click="adicionar" type="button">adicionar</button>
        </div>
        <label>
            Mostrar
            <input v-model="mostra" type="checkbox">
        </label>
        <div v-if="mostra"> {{ mensagem2 }} </div>
        <div v-for="(item, indice) in mensagens" :key="indice" > {{ item }} </div>
        <div>
            <label>
                Temperatura
                <input v-model.number="temperatura" type="number">
            </label>
        </div>
        <div>
            <label>
                Sensação
                <input :value="sensacao" 
                @input="(event) => sensacao = event.target.value"
                :style="{
                    fontWeight : temperatura * 30,
                }"
                :class="{
                    red: sensacao === 'quente',
                    orange: sensacao === 'morno',
                    blue: sensacao === 'frio',
                }"
                    >
            </label>
        </div>
        </div>
</template>

<script>
export default {

     props: {
    titulo: {
      type: String,
    },
    subtitulo: {
      type: String,
      default: 'Valor default'
    },
    temSubtitulo: {
      type: Boolean,
    },
  },

    data() {
        return {
            mensagem: 'olá mundo',
            mensagem2: 'olá mundo 2',
            mostra: true,
            mensagens: [
                'mensagem 1',
                'mensagem 2',
                'mensagem 3',
            ],
            temperatura: 25,
            //sensacao:'morno',
        }
    },
    methods: {
        adicionar(){
            this.mensagens.push(this.mensagem)
            this.mensagem = '' 
        },
        perdeuFoco() {
            console.log('perdi foco')
        },
        printar(mensagem) {
            console.log('filho ', mensagem)
        },
    },
    watch: {
        temperatura() {
            this.$emit('trocarTemperatura', this.temperatura) 
        },
    },

    computed: {
        sensacao: {
            get() {
                if (this.temperatura >= 30) {
                    return 'quente'
                } else if (this.temperatura > 20 ) {
                    return 'morno'
                } else {
                    return 'frio'
                }       
            },
            set(sensacao) {
                if (sensacao === 'quente') {
                this.temperatura = 30
                } else if (sensacao === 'morno') {
                this.temperatura = 25
                } else if (sensacao === 'frio') {
                this.temperatura = 20
                }
            },
        },
    }
 }
</script>

<style>
.red {
    color: red;
}
.orange {
    color: orange;
}
.blue {
    color: blue;
}
.bold {
    font-weight: bold;
}
</style>