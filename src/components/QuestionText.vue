<script setup lang="ts">
import { defineModel } from 'vue'
const model = defineModel<string | null>()
</script>

<template>
  <label for="exampleFormControlInput" class="form-label"> Combien de pattes a un chat ? </label>
  <input
    id="exampleFormControlInput"
    v-model="model"
    class="form-control"
    placeholder="Veuillez saisir un nombre"
  />
</template>
