<template>
  <main class="columns is-gapless is-multiline" :class="{'modo-escuro': modoEscuroAtivo}">
    <div class="column is-one-quarter">
      <BarraLateral @aoTemaAlterado="trocarTema"/>
    </div>
    <div class="column is-three-quarter conteudo">
      <FormularioTarefas @aoSalvarTarefa="salvarTarefa"/>
      <TarefaLista v-for="(tarefa, index) in tarefas" :key="index" :tarefa="tarefa"/>
        <BoxDiv v-if="listaVazia">
          Você ainda não realizou uma tarefa
        </BoxDiv>
    </div>

  </main>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import BarraLateral from './components/BarraLateral.vue';
import FormularioTarefas from './components/FormularioTarefas.vue';
import TarefaLista from './components/TarefaLista.vue';
import ITarefa from './Interfaces/ITarefa';
import BoxDiv from './components/BoxDiv.vue';


export default defineComponent({
  name: 'App',
  components: {
    BarraLateral,
    FormularioTarefas,
    TarefaLista,
    BoxDiv
  },
  data () {
    return {
      tarefas: [] as ITarefa[],
      modoEscuroAtivo: false
    }
  },
  computed: {
    listaVazia () : boolean {
      return this.tarefas.length === 0;
    }
    },
  methods:{
    salvarTarefa(tarefa: ITarefa){
      this.tarefas.push(tarefa)
    },
    trocarTema (modoEscuroAtivo: boolean){
      this.modoEscuroAtivo = modoEscuroAtivo
    }
  }
});
</script>

<style>
.lista{
  padding: 1.25rem;
}
main {
  --bg-primario: #fff;
  --texto-primario: #000;
}

main.modo-escuro{
  --bg-primario: #2b2d42;
  --texto-primario: #ddd;
}

.conteudo {
  background-color: var(--bg-primario);
}

</style>
