<template>
    <div class="is-flex is-align-items-center is-justify-content-space-between">
      <Cronometro :tempoEmSegundos="tempoEmSegundos" />
      <Botao
        @clickButton="start"
        icon="fas fa-play"
        text="play"
        :disabled="cronometroRodando"
      />
      <Botao
        @clickButton="ending"
        icon="fas fa-stop"
        text="stop"
        :disabled="!cronometroRodando"
      />
    </div>
  </template>
  <script lang="ts">
  import { defineComponent } from "vue";
  import Cronometro from "./Cronometro.vue";
  import Botao from "./Botao.vue";
  export default defineComponent({
    name: "Temporizador-Task",
    components: {
      Cronometro,
      Botao,
    },
    data() {
      return {
        tempoEmSegundos: 0,
        cronometro: 0,
        cronometroRodando: false,
      };
    },
    methods: {
      start() {
        this.cronometroRodando = true;
        this.cronometro = setInterval(() => {
          this.tempoEmSegundos += 1;
        }, 1000);
      },
      ending() {
        this.cronometroRodando = false;
        clearInterval(this.cronometro);
        this.$emit("aoTemporizadorFinalizado", this.tempoEmSegundos);
        this.tempoEmSegundos = 0;
      },
    },
  });
  </script>
  