<template>
    <header>
      <h1>
        <img src="../assets/logo.png" alt="logo do alura tracker" />
      </h1>
      <button class="button" @click="alterarTema">
        {{ textoBotao }}
      </button>
    </header>
  </template>
  <script lang="ts">
  import { defineComponent } from "vue";
  export default defineComponent({
    name: "BarraLateral",
    emits: ["aoTemaAlterado"],
    data() {
      return {
        modoEscuroAtivo: false,
      };
    },
    computed: {
      textoBotao() {
        if (this.modoEscuroAtivo) {
          return "Desativar modo escuro";
        }
        return "Ativar modo escuro";
      },
    },
    methods: {
      alterarTema(): void {
        this.$emit("aoTemaAlterado", this.modoEscuroAtivo);
        this.modoEscuroAtivo = !this.modoEscuroAtivo;
      },
    },
  });
  </script>
  <style scoped>
  header {
    padding: 1rem;
    background-color: var(--barra-primaria);
    width: 100%;
    height: 100vh;
    text-align: center;
  }
  h1 {
    margin-bottom: 32px;
  }
  @media only screen and (max-width: 768px) {
    header {
      padding: 2.5rem;
      height: auto;
    }
  }
  </style>