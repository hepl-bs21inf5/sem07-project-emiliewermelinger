<script setup lang="ts">
import QuestionRadio from '@/components/QuestionRadio.vue'
import QuestionCheckbox from './QuestionCheckbox.vue'
import QuestionSelect from './QuestionSelect.vue'
import QuestionText from './QuestionText.vue'
import { QuestionState } from '@/utils/models'
import { computed, ref, onMounted } from 'vue'

interface QuestionDetail {
  id: string
  image?: string
  answerDetail: string
}

//const questionIndices= ref([0, 1, 2]);
const questionIndices = ref(['habitants', 'horloge', 'escalier'])

const questionDetails = ref<QuestionDetail[]>([
  {
    id: 'horloge',
    image: "https://upload.wikimedia.org/wikipedia/commons/7/70/Horloge_Palud%2C_major_Davel_%28cropped%29.jpg",
    answerDetail: "L'horloge a été construite en 1964 puis rénovée en 2005",
  },
  {
    id: 'escalier',
    image: "https://upload.wikimedia.org/wikipedia/commons/thumb/0/09/Tour_de_Sauvabelin_Lausanne.jpg/520px-Tour_de_Sauvabelin_Lausanne.jpg",
    answerDetail: "La tour de Sauvabelin a 302 marches d'escalier",
  },
  { id: 'habitants',
    image: '',
    answerDetail:"En 2021 il y avait 140619 habitants à Lausanne, aujourd'hui il y en a plus de 150000",
  }
])

const filled = computed<boolean>(() =>
  questionStates.value.every((state) => state === QuestionState.Fill),
)
const submitted = computed<boolean>(() =>
  questionStates.value.every(
    (state) => state === QuestionState.Correct || state === QuestionState.Wrong,
  ),
)

const questionStates = ref<QuestionState[]>([])
const score = computed<number>(
  () => questionStates.value.filter((state) => state === QuestionState.Correct).length,
)
const totalScore = computed<number>(() => questionStates.value.length)

function reset(event: Event): void {
  event.preventDefault()
  questionStates.value = questionStates.value.map(() => QuestionState.Empty)
}

function submit(event: Event): void {
  event.preventDefault()
  questionStates.value = questionStates.value.map(() => QuestionState.Submit)
}

// Fonction pour mélanger aléatoirement les questions
const shuffleQuestions = (array: string[]): string[] => {
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

const getQuestionDetails = (id: string): QuestionDetail | undefined => {
  return questionDetails.value.find((detail) => detail.id === id)
}

onMounted(() => {
  questionIndices.value = shuffleQuestions([...questionIndices.value])
  questionStates.value = new Array(questionIndices.value.length).fill(QuestionState.Empty)
})
</script>

<template>
  <form @submit="submit">
    <div v-for="(id, idx) in questionIndices" :key="id">
      <h4>Question {{ idx + 1 }}</h4>

      <!-- Question Radio -->
      <QuestionRadio
        v-if="id === 'habitants'"
        id="habitants"
        v-model="questionStates[idx]"
        answer="140619"
        text="Combien y avait t-il d'habitants à Lausanne en 2021?"
        :options="[
          { value: '140619', text: '140619' },
          { value: '125063', text: '125063' },
          { value: '150720', text: '150720' },
          { value: '145015', text: '145015' },
        ]"/>
      <QuestionRadio
        v-if="id === 'horloge'"
        id="horloge"
        v-model="questionStates[idx]"
        answer="1964"
        text="En quelle année a été construite l'horloge parlante de la place de la Palud?"
        :options="[
          { value: '1964', text: '1964' },
          { value: '1970', text: '1970' },
          { value: '1965', text: '1965' },
          { value: '1963', text: '1963' },
        ]"/>
      <QuestionRadio
        v-if="id === 'escalier'"
        id="escalier"
        v-model="questionStates[idx]"
        answer="302"
        text="Combien de marches a la tour de Sauvabelin ?"
        :options="[
          { value: '302', text: '302' },
          { value: '307', text: '307' },
          { value: '299', text: '299' },
          { value: '296', text: '296' },
        ]"/>
      <div
        v-if="
          questionStates[idx] === QuestionState.Correct ||
          questionStates[idx] === QuestionState.Wrong
        "
      >
      <div class="answer-detail">
        <p v-if="getQuestionDetails(id)?.answerDetail?.trim()">
            {{ getQuestionDetails(id)?.answerDetail }}
          </p>

        </div>
        <img
          v-if="getQuestionDetails(id)?.image"
          :src="getQuestionDetails(id)?.image"
          alt="Détail de la réponse"
          class="question-image"
        />
      </div>
    </div>

    <QuestionText
      id="lac"
      v-model="questionStates[3]"
      answer="['leman','léman','le lac léman','le lac leman']"
      text="Comment s'appelle le lac qui touche Lausanne ?"
      answer-detail="Contrairement à ce que certains disent, le vrai nom du lac est le lac léman et non le lac de Genève"
    />

    <QuestionSelect
      id="tourisme"
      v-model="questionStates[4]"
      answer="Le siège du comité international olympique"
      text="Lausanne est connue pour :"
      :options="[
        {
          value: 'Le siège du comité international olympique',
          text: 'Le siège du comité international olympique',
        },
        { value: 'lac', text: 'Le lac' },
        { value: 'chocolat', text: 'Le chocolat du Barbare' },
        { value: 'Sa cathédrale', text: 'Sa cathédrale' },
      ]"
      answer-detail="Lausanne est connue car c'est la capitale olympique"
    />

    <QuestionCheckbox
      id="metro"
      v-model="questionStates[5]"
      :answer="['m1', 'm2']"
      text="Comment s'appellent les métros que l'on peut emprunter à Lausanne ?"
      :options="[
        { value: 'm1', text: 'm1' },
        { value: 'm2', text: 'm2' },
        { value: 'n1', text: 'n1' },
        { value: 'tram', text: 'tram' },
      ]"
      answer-detail="Les métros se nomment m1 et m2. Le m veut dire métro et le numéro est l'ordre dans lequel ils ont été construits "
    />

    <br />
    <button class="btn btn-primary" :class="{ disabled: !filled }" @click="submit">Terminer</button>
    &nbsp;
    <button class="btn btn-secondary" @click="reset">Réinitialiser</button>
    <div v-if="submitted">Score : {{ score }} / {{ totalScore }}</div>
    <!--affiche le score uniquement si toutes les questions ont étés soumises et corrigées-->

    <div>Debug états : {{ questionStates }}</div>
    <!--permet de debug facilement l'application -->
  </form>
</template>


