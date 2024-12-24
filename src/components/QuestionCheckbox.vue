<script setup lang="ts">
import { ref, watch, type PropType } from "vue";
import { QuestionState } from "@/utils/models";

const model = defineModel<QuestionState>();
const props = defineProps({
  id: { type: String, required: true },
  text: { type: String, required: true },
  options: {
    type: Array as PropType<Array<{ value: string; text: string }>>,
    required: true,
  },
  answerDetail: { type: String, default: '' },
  answer: { type: Array as PropType<string[]>, required: true}, // Réponses multiples
});

const values = ref<string[]>([]); // Tableau de réponses sélectionnées

function arraysEqual(arr1: string[], arr2: string[]): boolean {
  if (arr1.length !== arr2.length) {
    return false;
  }
  return arr1.every((value) => arr2.includes(value));
}


watch(
  model,
  (newModel) => {
    if (newModel === QuestionState.Submit) {
      const isCorrect =arraysEqual([...values.value], [...props.answer]);
      model.value = isCorrect ? QuestionState.Correct : QuestionState.Wrong;
        //JSON.stringify([...values.value].sort()) === JSON.stringify([...props.answer].sort());
      //model.value = isCorrect ? QuestionState.Correct : QuestionState.Wrong;
    } else if (newModel === QuestionState.Empty) {
      values.value = [];
    }
  },
  {immediate:true},
);

watch(
  values,
  (newValues) => {
    if (newValues.length === 0) {
      model.value = QuestionState.Empty;
    } else {
      model.value = QuestionState.Fill;
    }
  },
  { immediate: true },
);
</script>

<template>
  {{ props.text }}
  <div v-for="option in props.options" :key="option.value" class="form-check">
    <input
      :id="`${props.id}-${option.value}`"
      v-model="values"
      class="form-check-input"
      type="checkbox"
      :value="option.value"
      :disabled="
        model === QuestionState.Submit ||
        model === QuestionState.Correct ||
        model === QuestionState.Wrong"
    />
    <label class="form-check-label" :for="`${props.id}-${option.value}`">
      {{ option.text }}
    </label>
  </div>
  <div
    v-if="model === QuestionState.Correct || model === QuestionState.Wrong"
  >
    <p v-if="model === QuestionState.Correct" class="text-success">Juste !</p>
    <p v-else class="text-danger">
      Faux ! Les réponses correctes étaient : {{ props.answer.join(", ") }}
    </p>
    <p class="blockquote-footer">{{ props.answerDetail }}</p>
  </div>
</template>
