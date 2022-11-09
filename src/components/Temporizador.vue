<template>
    <div class="is-flex is-align-items-center is-justify-content-space-between">
        <Cronometro :tempoEmSegundos="tempoEmSegundos" />
        <BotaoCronometro
            icone="fas fa-play"
            nomeBotao="Play"
            :botaoDesabilitado="cronometroRodando"
            @clicado="iniciar"
        />
        <BotaoCronometro
            icone="fas fa-stop"
            nomeBotao="Stop"
            :botaoDesabilitado="!cronometroRodando"
            @clicado="finalizar"
        />
    </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import Cronometro from './Cronometro.vue';
import BotaoCronometro from './BotaoCronometro.vue';

export default defineComponent({
    name: 'Temporizador',
    emits: [
        'aoTemporizadorFinalizado'
    ], // variavel responsavel por emitir o estado atual do tempo
    components: {
        Cronometro,
        BotaoCronometro,
    },
    data() {
        return {
            tempoEmSegundos: 0,
            cronometro: 0,
            cronometroRodando: false,
        };
    },
    methods: {
        iniciar() {
            this.cronometroRodando = true
            this.cronometro = setInterval(() => {
                this.tempoEmSegundos += 1;
            }, 1000);
        },
        finalizar() {
            this.cronometroRodando = false
            clearInterval(this.cronometro)
            this.$emit('aoTemporizadorFinalizado', this.tempoEmSegundos)
            this.tempoEmSegundos = 0
        },
    },
});
</script>
