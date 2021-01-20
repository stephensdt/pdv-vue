<template>
    <div>
        <h3> {{ titulo }}</h3>
        <h4 v-if="temSubtitulo">{{ subtitulo }}</h4>
        <div>{{ mensagem }}</div>
        <div>
            <input v-model="mensagem" @blur="perdeuFoco">
            <button v-on:click="adicionar" type="button">adicionar</button>
        </div>
        <label>
            Mostrar
            <input v-model="mostra" type="checkbox">
        </label>
        <div v-if="mostra"> {{ mensagem2 }} </div>
        <div>
        <label>
            Temperatura
            <input v-model.number="temperatura" type="number" >
        </label>
        </div>
        <div>
        <label>
            Sensação
            <input
            :value="sensacao"
            @input="(event) => sensacao = event.target.value"
            >
        </label>
        </div>
    </div>
</template>

<script lang="ts">
import { Vue, Component, Prop } from 'vue-property-decorator'

@Component
export default class ComponenteComClasse extends Vue {
    @Prop({ type: String }) titulo!: string
    @Prop({ type: String, default: 'Valor default' }) subtitulo!: string
    @Prop({ type: Boolean }) temSubtitulo!: boolean

    mensagem = 'Olá Mundo!'
    mensagem2 = 'Olá Mundo2!'
    mostra = false
    mensagens = [
                'mensagem 1',
                'mensagem 2',
                'mensagem 3',
    ]
    temperatura = 25

    get sensacao(): Sensacao {
        if (this.temperatura >= 30) {
          return 'quente'
        } else if (this.temperatura > 20 ) {
          return 'morno'
        } else {
          return 'frio'
        }       
    }

    set sensacao(sensacao) {
        if (sensacao === 'quente') {
            this.temperatura = 30
        } else if (sensacao === 'morno') {
            this.temperatura = 25
        } else if (sensacao === 'frio') {
            this.temperatura = 20
        }
    }

    adicionar(){
            this.mensagens.push(this.mensagem)
            this.mensagem = '' 
    }
    perdeuFoco() {
            console.log('perdi foco')
    }
    printar(mensagem: any) {
            console.log('filho ', mensagem)
        }
}

type Sensacao = 'quente' | 'morno' | 'frio';

</script>