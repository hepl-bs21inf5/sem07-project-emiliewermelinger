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
        answer-detail="Une année bissextile comporte 366 jours et une non bissextile 365"
      />
    <QuestionRadio
      v-if="index===1"
      id="hep"
      v-model="questionStates[1]"
      answer="9"
      text="Combien y a-t-il de bâtiments de la Hep à l'avenue de Cour 33?"
      :options="[
        { value: '9', text: '9' },
        { value: '8', text: '8' },
        { value: '10', text: '10' },
        { value: '7', text: '7' },
      ]"
      answer-detail="La Hep a 9 bâtiments en comptant l'aula"
    />
    <QuestionRadio
      v-if="index===2"
      id="titi"
      v-model="questionStates[2]"
      answer="titi"
      text=" Quelle est le nom de l'oiseau que Gros-minet veut manger ?"
      :options="[
        { value: 'titi', text: 'Titi' },
        { value: 'Lulu', text: 'Lulu' },
        { value: 'momo', text: 'Momo' },
        { value: 'fafa', text: 'Fafa' },
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
      id="chien"
      v-model="questionStates[4]"
      answer="chien"
      text="Quel est l'animal qui représente Snoopy ?"
      :options="[
        { value: 'chien', text: 'Chien' },
        { value: 'chat', text: 'Chat' },
        { value: 'souris', text: 'Souris' },
        { value: 'oiseau', text: 'Oiseau' }
      ]"
      answer-detail="Snoopy est un chien noir et blanc"
    />
    <QuestionSelect
      id="garfield"
      v-model="questionStates[5]"
      answer="orange"
      text="De quelle couleur est Garfield ?"
      :options="[
        { value: 'bleu', text: 'Bleu' },
        { value: 'orange', text: 'Orange' },
        { value: 'jaune', text: 'Jaune' },
        { value: 'violet', text: 'Violet' }
      ]"
      answer-detail="Garfield est un chat orange qui adore les lasagnes"
    />

    <QuestionCheckbox
      id="ecole"
      v-model="questionStates[6]"
      :answer="['Allemand', 'Français','Anglais']"
      text="Quelles sont les langues obligatoires apprises à l'école en Suisse ?"
      :options="[
        { value: 'Allemand', text: 'Allemand' },
        { value: 'Français', text: 'Français' },
        { value: 'Anglais', text: 'Anglais' },
        { value: 'Italien', text: 'Italien' },
      ]"
      answer-detail="Les élèves apprennent trois langues principales, l'Allemand, le Français et l'Anglais et l'Italien est en option"
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

