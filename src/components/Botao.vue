<template>
    <button class="button" @click="clickButton" :disabled="disabled">
      <span class="icon">
        <i :class="icon"></i>
      </span>
      <span>{{ text }}</span>
    </button>
  </template>
  <script lang="ts">
  import { defineComponent } from "vue";
  export default defineComponent({
    name: "Button-Control",
    emits: ["clickButton"],
    props: {
      disabled: {
        type: Boolean,
      },
      icon: {
        type: String,
        required: true,
      },
      text: {
        type: String,
        required: true,
      },
    },
    methods: {
      clickButton(): void {
        this.$emit("clickButton");
      },
    },
  });
  </script>
  