<script setup lang="ts">
import QuestionRadio from '@/components/QuestionRadio.vue'
import { computed, ref } from 'vue'

const cheval = ref<string | null>(null)
const chat = ref<string | null>(null)
const capitale = ref<string | null>(null)
const filled = computed<boolean>(
  () => cheval.value !== null && chat.value !== null && capitale.value !== null,
)
const annee = ref<string | null>(null)

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
  const max_score = 3
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
      v-model="annee"
      text="Combien de jours comporte une année non-bissextile ?"
      :options="[
        { value: '265', text: '265' },
        { value: '365', text: '365' },
        { value: '100', text: '100' },
        { value: '366', text: '366' },
      ]"
    />
    De quelle couleur est le cheval blanc de Napoléon ?
    <div class="form-check">
      <input
        id="chevalBlanc"
        v-model="cheval"
        class="form-check-input"
        type="radio"
        name="cheval"
        value="blanc"
      />
      <label class="form-check-label" for="chevalBlanc">Blanc</label>
    </div>
    <div class="form-check">
      <input
        id="chevalcoloré"
        v-model="cheval"
        class="form-check-input"
        type="radio"
        name="cheval"
        value="arc-en-ciel"
      />
      <label class="form-check-label" for="chevalcoloré">arc-en-ciel</label>
    </div>
    <div class="form-check">
      <input
        id="chevalBrun"
        v-model="cheval"
        class="form-check-input"
        type="radio"
        name="cheval"
        value="brun"
      />
      <label class="form-check-label" for="chevalBrun">Brun</label>
    </div>
    <div class="form-check">
      <input
        id="chevalNoir"
        v-model="cheval"
        class="form-check-input"
        type="radio"
        name="cheval"
        value="noir"
      />
      <label class="form-check-label" for="chevalNoir">Noir</label>
    </div>
    Combien de pattes a un chat ?
    <div class="form-check">
      <input
        id="pattes1"
        v-model="chat"
        class="form-check-input"
        type="radio"
        name="chat"
        value="5"
      />
      <label class="form-check-label" for="pattes1">5</label>
    </div>
    <div class="form-check">
      <input
        id="pattes4"
        v-model="chat"
        class="form-check-input"
        type="radio"
        name="chat"
        value="2"
      />
      <label class="form-check-label" for="pattes4">2</label>
    </div>
    <div class="form-check">
      <input
        id="pattes2"
        v-model="chat"
        class="form-check-input"
        type="radio"
        name="chat"
        value="7"
      />
      <label class="form-check-label" for="pattes2">7</label>
    </div>
    <div class="form-check">
      <input
        id="pattes3"
        v-model="chat"
        class="form-check-input"
        type="radio"
        name="chat"
        value="4"
      />
      <label class="form-check-label" for="pattes3">4</label>
    </div>
    Quelle est la capitale de la Suisse ?
    <div class="form-check">
      <input
        id="capitale1"
        v-model="capitale"
        class="form-check-input"
        type="radio"
        name="Zürich"
        value="Zürich"
      />
      <label class="form-check-label" for="capitale1">Zürich</label>
    </div>
    <div class="form-check">
      <input
        id="capitale4"
        v-model="capitale"
        class="form-check-input"
        type="radio"
        name="Lausanne"
        value="Lausanne"
      />
      <label class="form-check-label" for="capitale4">Lausanne</label>
    </div>
    <div class="form-check">
      <input
        id="capitale2"
        v-model="capitale"
        class="form-check-input"
        type="radio"
        name="Genève"
        value="Genève"
      />
      <label class="form-check-label" for="capitale2">Genève</label>
    </div>
    <div class="form-check">
      <input
        id="capitale3"
        v-model="capitale"
        class="form-check-input"
        type="radio"
        name="Berne"
        value="Berne"
      />
      <label class="form-check-label" for="capitale3">Berne</label>
    </div>
    <button class="btn btn-primary" :class="{ disabled: !filled }" type="submit">Terminer</button>
    <button class="btn btn-secondary" @click="reset">Réinitialiser</button>
  </form>
</template>
