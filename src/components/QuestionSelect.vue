<script setup lang="ts">
  import { ref,watch, type PropType } from "vue";
  import { QuestionState } from '@/utils/models'

  const model = defineModel<QuestionState>();
  const props = defineProps({
    id: { type: String, required: true },
    text: { type: String, required: true },
    options: {type: Array as PropType<Array<{ value: string; text: string }>>,required: true,},
    answerDetail:{type: String, default:''},
    answer:{type: String,required: true,},
  });

  const value= ref<string| null>(null)

  watch(  //si la réponse est juste., cela deviendra Correct et sinon Wrong -> seulement si l'état de la question est Submit
    model,
    (newModel) => {
      if (newModel === QuestionState.Submit) {
        model.value = value.value === props.answer ? QuestionState.Correct : QuestionState.Wrong
    }else if (newModel === QuestionState.Empty) {
      value.value = null
    }
  },
);
  watch( //permet de mettre à jour la valeur, si null -> empty, sinon Fill
    value,
    (newValue)=>{
      if (newValue===null){
        model.value = QuestionState.Empty
      }else{
        model.value = QuestionState.Fill
      }
    },
    {immediate: true},
  )
</script>

<template>
  <div>
    <p>{{ props.text }}</p>
    <select
      v-model="value"
      :disabled="model === QuestionState.Submit || model === QuestionState.Correct || model === QuestionState.Wrong"
      class="form-select"
    >
    <option value=disabled>Choisissez une réponse</option>
      <option
        v-for="option in props.options"
        :key="option.value"
        :value="option.value"
      >
        {{ option.text }}
      </option>
    </select>
    <div v-if="model === QuestionState.Correct || model === QuestionState.Wrong">
      <p v-if="model === QuestionState.Correct" class="text-success">Juste !</p>
      <p v-else class="text-danger">
        Faux ! La réponse était : {{ props.answer }}
      </p>
     <p class="blockquote-footer">{{ props.answerDetail }}</p>
    </div>
  </div>
</template>
<style scoped>
  .text-danger {
    color: purple !important;
  }
</style>
