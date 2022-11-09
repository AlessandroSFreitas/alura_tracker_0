<template>
    <button class="button" @click="clicado" :disabled="botaoDesabilitado">
        <span class="icon">
            <i :class="icone"></i>
        </span>
        <span>{{ nomeBotao }}</span>
    </button>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
    name: 'BotaoCronometro',
    emits : [
        'clicado'
    ],
    props: {
        icone: {
            type: String,
            required: true
        },
        nomeBotao: {
            type: String,
            required: true
        },
        botaoDesabilitado: {
            type: Boolean,
            required: true
        },
    },
    methods: {
        clicado () : void {
            this.$emit('clicado')
        }
    },
})
</script>
