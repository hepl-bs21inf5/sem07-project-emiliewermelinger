<script setup lang="ts">
  import { defineModel, defineProps } from "vue";

  const model = defineModel<string | null>();
  const props = defineProps({
    id: { type: String, required: true },
    text: { type: String, required: true },
    placeholder:{type: String, default : "Veuillez saisir une réponse"}
  });
</script>

<template>
  <div>
    <label for="exampleFormControlInput" class="form-label">{{ props.text }}</label>
    <input
      id="exampleFormControlInput"
      v-model="model"
      class="form-control"
      :placeholder="props.placeholder"
  />
</div>
</template>
