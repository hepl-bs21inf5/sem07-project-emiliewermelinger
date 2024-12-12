<script setup lang="ts">
import QuestionRadio from '@/components/QuestionRadio.vue'
import QuestionText from './QuestionText.vue'
import { computed, ref } from 'vue'

const cheval = ref<string | null>(null)
const chat = ref<string | null>(null)
const capitale = ref<string | null>(null)
const filled = computed<boolean>(
  () => cheval.value !== null && chat.value !== null && capitale.value !== null,
)
const annee = ref<string | null>(null)
const correctAnswers= ref<boolean[]>([])


function reset(event: Event): void {
  event.preventDefault()
  cheval.value = null
  chat.value = null
  capitale.value = null
  annee.value = null
}

function submit(event: Event): void {
  event.preventDefault()
  let score = 0
  const max_score = 4
  if (filled.value) {
    if (cheval.value == 'blanc') {
      score += 1
    }
    //il faut mettre une parenthèse après le if pour dire sur quoi fait le if
    //les accolades permettent de dire quoi faire si le if est juste
    if (chat.value == '4') {
      score += 1
    }
    // les accolade autour de "chat.value" sont nécessaires seulement lorsque on met du texte et que l'on veut qu'il affiche la valeur enregistrée dans "chat.value"

    if (capitale.value == 'Berne') {
      score += 1
    }

    if (annee.value == '365') {
      score += 1
    }

    if (score == max_score) {
      alert('Vous avez fait tout juste! Bravo')
    } else {
      alert(`Vous avez fait ${score} bonnes réponses`)
    }
  }
}
</script>

<template>
  <form @submit="submit">
    <QuestionRadio
      id="année"
      v-model="correctAnswers[0]"
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
      id="chevalBlanc"
      v-model="correctAnswers[1]"
      answer="blanc"
      text="De quelle couleur est le cheval blanc de Napoléon ?"
      :options="[
        { value: 'blanc', text: 'Blanc' },
        { value: 'arc-en-ciel', text: 'Arc-en-ciel' },
        { value: 'brun', text: 'Brun' },
        { value: 'noir', text: 'Noir' },
      ]"
    />

    <QuestionText
      id="chat"
      v-model="chat"
      text="Combien de pattes a un chat ?"
    />

    <QuestionRadio
      id="capitale"
      v-model="correctAnswers[2]"
      answer="Berne"
      text=" Quelle est la capitale de la Suisse ?"
      :options="[
        { value: 'Berne', text: 'Berne' },
        { value: 'Lausanne', text: 'Lausanne' },
        { value: 'Zürich', text: 'Zürich' },
        { value: 'Genève', text: 'Genève' },
      ]"
    />
    <button class="btn btn-primary" :class="{ disabled: !filled }" type="submit">Terminer</button>
    <button class="btn btn-secondary" @click="reset">Réinitialiser</button>
    <div>Réponses correctes:{{ correctAnswers }}</div>
  </form>
</template>

