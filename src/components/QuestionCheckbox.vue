<script setup lang="ts">
  import { defineProps,defineModel, type PropType } from "vue";

  const modelValue = defineModel<string[]>();
  defineProps({
    id: { type: String, required: true },
    text: { type: String, required: true },
    options: {
      type: Array as PropType<Array<{ value: string; text: string }>>,
      required: true,
    },
  });
</script>

<template>
  <div
  v-for="(option, index) in options"
  :key="index"
  class="form-check"
  >
    <input
      :id="'checkbox-${option}'"
      v-model="modelValue"
      class="form-check-input"
      type="checkbox"
      :value="option.value"
    />
    <label
      class="form-check-label"
      :for="`checkbox-${option}`"
    >
      {{ option }}
    </label>
  </div>
</template>
