<script setup lang="ts">
import { ref, watch, type PropType, onMounted, computed } from 'vue'
import { QuestionState } from '@/utils/models'

const model = defineModel<QuestionState>()
const props = defineProps({
  id: { type: String, required: true },
  text: { type: String, required: true },
  options: {
    type: Array as PropType<Array<{ value: string; text: string }>>,
    required: true,
  },
  answerDetail: { type: String, default:'' },
  answer: { type: String, required: true },
})

const value = ref<string | null>(null)
const shuffledOptions = ref<Array<{ value: string; text: string }>>([])

// la fonction shuffleOptions prend un tableau d'options et les mélange aléatoirement
const shuffleOptions = (array: Array<{ value: string; text: string }>) => {
  let currentIndex = array.length,
    randomIndex,
    temporaryValue
  while (currentIndex !== 0) {
    randomIndex = Math.floor(Math.random() * currentIndex)
    currentIndex -= 1
    temporaryValue = array[currentIndex]
    array[currentIndex] = array[randomIndex]
    array[randomIndex] = temporaryValue
  }
  return array
}
// Applique le mélange des options lors du montage
onMounted(() => {
  shuffledOptions.value = shuffleOptions([...props.options])
})

watch(
  //si la réponse est juste., cela deviendra Correct et sinon Wrong -> seulement si l'état de la question est Submit
  model,
  (newModel) => {
    if (newModel === QuestionState.Submit) {
      model.value = value.value === props.answer ? QuestionState.Correct : QuestionState.Wrong
    } else if (newModel === QuestionState.Empty) {
      value.value = null
    }
  },
)
watch(
  //permet de mettre à jour la valeur, si null -> empty, sinon Fill
  value,
  (newValue) => {
    if (newValue === null) {
      model.value = QuestionState.Empty
    } else {
      model.value = QuestionState.Fill
    }
  },
  { immediate: true },
)

// Computed pour obtenir le texte de la réponse associée
const answerText = computed<string>(
  () =>
    props.options.find((option) => option.value === props.answer)?.text ??
    props.answer,
)
</script>

<template>
  {{ props.text }}
  <div v-for="option in shuffledOptions" :key="option.value" class="form-check">
    <input
      :id="`${props.id}-${option.value}`"
      v-model="value"
      class="form-check-input"
      type="radio"
      :name="props.id"
      :value="option.value"
      :disabled="
        model === QuestionState.Submit ||
        model === QuestionState.Correct ||
        model === QuestionState.Wrong
      "
    />
    <label class="form-check-label" :for="`${props.id}-${option.value}`">
      {{ option.text }}
    </label>
  </div>
  <div v-if="model === QuestionState.Correct || model === QuestionState.Wrong">
    <p v-if="model === QuestionState.Correct" class="text-success">Juste !</p>
    <p v-else class="text-danger">Faux ! La réponse était : {{ answerText }}</p>
    <p class="blockquote-footer">{{ props.answerDetail }}</p>
  </div>
</template>
<style scoped>
.text-danger {
  color: purple !important;
}
</style>
