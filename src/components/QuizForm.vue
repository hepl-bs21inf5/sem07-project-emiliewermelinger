<script setup lang="ts">
import QuestionRadio from '@/components/QuestionRadio.vue'
import QuestionCheckbox from './QuestionCheckbox.vue'
import QuestionSelect from './QuestionSelect.vue'
import QuestionText from './QuestionText.vue'
import { QuestionState } from '@/utils/models'
import { computed, ref, onMounted } from 'vue'

const questionIndices= ref([0, 1, 2]);


const filled = computed<boolean>(
  () => questionStates.value.every(state => state === QuestionState.Fill),
)
const submitted = computed<boolean>(() =>
  questionStates.value.every(
    state => state === QuestionState.Correct || state === QuestionState.Wrong,
  ),
)

const questionStates = ref<QuestionState[]>([])
const score = computed<number>(() =>
    questionStates.value.filter(state => state === QuestionState.Correct)
      .length,
)
const totalScore =computed<number>(() => questionStates.value.length);


function reset(event: Event): void {
  event.preventDefault()
  questionStates.value = questionStates.value.map(() => QuestionState.Empty)
}

function submit(event: Event): void {
  event.preventDefault()
  questionStates.value = questionStates.value.map(() => QuestionState.Submit)
}

// Fonction pour mélanger aléatoirement les questions
const shuffleQuestions = (array:number[]):number[] => {
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

onMounted(() => {
  questionIndices.value = shuffleQuestions([...questionIndices.value]);
});

</script>

<template>
  <form @submit="submit">
    <div v-for="index in questionIndices" :key="index">
      <!-- Question Radio -->
      <QuestionRadio
        v-if="index===0"
        id="année"
        v-model="questionStates[0]"
        answer="365"
        text="Combien de jours comporte une année non-bissextile ?"
        :options="[
          { value: '265', text: '265' },
          { value: '365', text: '365' },
          { value: '100', text: '100' },
          { value: '366', text: '366' },
        ]"
      />
    <QuestionRadio
      v-if="index===1"
      id="chevalBlanc"
      v-model="questionStates[1]"
      answer="blanc"
      text="De quelle couleur est le cheval blanc de Napoléon ?"
      :options="[
        { value: 'blanc', text: 'Blanc' },
        { value: 'arc-en-ciel', text: 'Arc-en-ciel' },
        { value: 'brun', text: 'Brun' },
        { value: 'noir', text: 'Noir' },
      ]"
    />
    <QuestionRadio
      v-if="index===2"
      id="capitale"
      v-model="questionStates[2]"
      answer="Berne"
      text=" Quelle est la capitale de la Suisse ?"
      :options="[
        { value: 'Berne', text: 'Berne' },
        { value: 'Lausanne', text: 'Lausanne' },
        { value: 'Zürich', text: 'Zürich' },
        { value: 'Genève', text: 'Genève' },
      ]"
    />
  </div>

    <QuestionText
      id="chat"
      v-model="questionStates[3]"
      answer="['4','quatre']"
      text="Combien de pattes a un chat ?"
      answer-detail="Le chat est un mammifère quadrupède."

    />


    <QuestionSelect
      id="questionFavori"
      v-model="questionStates[4]"
      answer="café"
      text="Quelle est votre boisson préférée ?"
      :options="[
        { value: 'café', text: 'Café' },
        { value: 'thé', text: 'Thé' },
        { value: 'eau', text: 'Eau' },
        { value: 'jus', text: 'Jus' }
      ]"
    />

    <QuestionCheckbox
      id="continents"
      v-model="questionStates[5]"
      :answer="['Afrique', 'Europe']"
      text="Quels continents font partie du monde ?"
      :options="[
        { value: 'Afrique', text: 'Afrique' },
        { value: 'Asie', text: 'Asie' },
        { value: 'Europe', text: 'Europe' },
        { value: 'Atlantide', text: 'Atlantide' },
      ]"
      answer-detail="Les continents corrects sont Afrique et Europe."
    />

      <br />
      <button
        class="btn btn-primary"
        :class="{ disabled: !filled }"
        @click="submit"
      >
        Terminer
      </button>
      &nbsp;
      <button class="btn btn-secondary" @click="reset">Réinitialiser</button>
      <div v-if="submitted">Score : {{ score }} / {{ totalScore }}</div> <!--affiche le score uniquement si toutes les questions ont étés soumises et corrigées-->
      <div>Debug états : {{ questionStates }}</div> <!--permet de debug facilement l'application -->
  </form>
</template>

