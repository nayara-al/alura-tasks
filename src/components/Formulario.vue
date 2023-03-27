<template>
    <div class="box formulario">
      <div class="columns">
        <div
          class="column is-7"
          role="form"
          aria-label="Formulário para criação de uma nova tarefa"
        >
          <input
            type="text"
            class="input is-rounded"
            placeholder="Qual tarefa deseja iniciar?"
            v-model="descricao"
          />
        </div>
        <div class="column">
          <Temporizador @aoTemporizadorFinalizado="finalizarTarefa" />
        </div>
      </div>
    </div>
  </template>
  <script lang="ts">
  import { defineComponent } from "vue";
  import Temporizador from "./Temporizador.vue";
  export default defineComponent({
    name: "Formulario-Total",
    emits: ["aoAdicionarTarefa"],
    components: {
      Temporizador,
    },
    data() {
      return {
        descricao: "",
      };
    },
    methods: {
      finalizarTarefa(tempoDecorrido: number): void {
        this.$emit("aoAdicionarTarefa", {
          duracaoEmSegundos: tempoDecorrido,
          descricao: this.descricao,
        });
        this.descricao = "";
      },
    },
  });
  </script>
  <style>
  .formulario {
    color: var(--texto-primario);
    background-color: var(--bg-primario);
  }
  </style>
  