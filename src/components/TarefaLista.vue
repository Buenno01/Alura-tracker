<template>
    <BoxDiv>
        <div class="columns">
            <div class="column is-7">
                    {{tarefa.descricao || 'Tarefa sem nome'}}
            </div>
            <div class="column">
                <CronometroForm :tempoEmSegundos="tarefa.duracaoEmSegundos"/>
            </div>
        </div>
    </BoxDiv> 
</template>

<script lang="ts">
import ITarefa from '@/Interfaces/ITarefa';
import CronometroForm from './CronometroForm.vue';
import BoxDiv from './BoxDiv.vue';
import { PropType, defineComponent } from 'vue';

export default defineComponent({
    name: 'TarefaLista',
    components:{
        CronometroForm,
        BoxDiv
    },
    props: {
        tarefa:{
            type: Object as PropType<ITarefa>,
            required: true
        }
    }
})

</script>

<style scoped>
.box{
    background: #faf0ca;
}
</style>