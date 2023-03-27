<template>
  <main
    class="columns is-gapless is-multiline"
    :class="{ 'modo-escuro': modoEscuroAtivo }"
  >
    <div class="column is-one-quarter">
      <BarraLateral @aoTemaAlterado="trocarTema" />
    </div>
    <div class="column is-three-quarter conteudo">
      <div class="controller">
        <Formulario @aoAdicionarTarefa="adicionarTarefa" />
        <Botao
          text="Limpar lista"
          icon="fa-solid fa-trash"
          class="button"
          @click="deletarLista"
        />
      </div>
      <div class="lista">
        <Tarefa
          v-for="(tarefa, index) in tarefas"
          :key="index"
          :tarefa="tarefa"
        />
        <Box v-if="listaEstaVazia"> Você não está muito produtivo hoje :( </Box>
      </div>
    </div>
  </main>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import BarraLateral from "./components/BarraLateral.vue";
import Botao from "./components/Botao.vue";
import Formulario from "./components/Formulario.vue";
import Box from "./components/Box.vue";
import Tarefa from "./components/Tarefa.vue";
import ITarefa from "./interfaces/ITarefa";
export default defineComponent({
  name: "App",
  components: {
    BarraLateral,
    Formulario,
    Tarefa,
    Box,
    Botao,
  },
  data() {
    return {
      tarefas: [] as ITarefa[],
      modoEscuroAtivo: false,
    };
  },
  mounted() {
    if (localStorage.getItem("tarefas")) {
      try {
        this.tarefas = JSON.parse(localStorage.getItem("tarefas") as string);
      } catch {
        console.log("lista vazia");
      }
    }
  },
  computed: {
    listaEstaVazia(): boolean {
      return this.tarefas.length === 0;
    },
  },
  methods: {
    adicionarTarefa(tarefa: ITarefa) {
      this.tarefas.push(tarefa);
      const parsed = JSON.stringify(this.tarefas);
      localStorage.setItem("tarefas", parsed);
    },
    trocarTema(modoEscuroAtivo: boolean) {
      this.modoEscuroAtivo = modoEscuroAtivo;
    },
    deletarLista() {
      console.log("fui clicado");
      localStorage.clear();
      window.location.reload();
    },
  },
});
</script>

<style>
.lista {
  padding: 1.25rem;
}
main {
  --bg-primario: #fff;
  --texto-primario: #000;
  --barra-primaria: #fcc34f;
}
main.modo-escuro {
  --bg-primario: #2b2d42;
  --texto-primario: #ddd;
  --barra-primaria: #211b5d;
}
.conteudo {
  background-color: var(--bg-primario);
}
</style>

<style scoped>
.controller {
  text-align: center;
}
</style>
