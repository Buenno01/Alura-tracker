<template>
    <div class="is-flex is-align-items-center is-justify-content-space-between">
        <CronometroForm :tempoEmSegundos="tempoEmSegundos" />

        <TemporizadorBtn @clicado="iniciar" icone="fas fa-play" texto="play" :desabilitado="cronometroAtivo" />
        <TemporizadorBtn @clicado="finalizar" icone="fas fa-stop" texto="stop" :desabilitado="!cronometroAtivo" />

    </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import CronometroForm from './CronometroForm.vue';
import TemporizadorBtn from './TemporizadorBtn.vue';

export default defineComponent({
    name: 'TemporizadorForm',
    emit: ['aoTemporizadorFinalizado'],
    components:{
        CronometroForm,
        TemporizadorBtn
    },
        data(){
            return {
                tempoEmSegundos: 0,
                cronometro: 0,
                cronometroAtivo: false,
            }
    },
    methods:{
        iniciar(){
            this.cronometroAtivo = true;
            this.cronometro = setInterval (() => {
                this.tempoEmSegundos++;
            }, 1000)
        },
        finalizar(){
            this.cronometroAtivo = false;
            clearInterval(this.cronometro);
            this.$emit('aoTemporizadorFinalizado', this.tempoEmSegundos);
            this.tempoEmSegundos = 0;
        }
    }
})
</script>