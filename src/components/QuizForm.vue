<script setup lang="ts">
import { computed, ref } from 'vue'

const cheval = ref<string | null>(null)
const chat = ref<string | null>(null)
const capitale = ref<string | null>(null)
const filled = computed<boolean>(() => cheval.value !== null)

function submit(event: Event): void {
  event.preventDefault()
  if (filled.value) {
    alert(
      `Vous avez choisi la couleur ${cheval.value},avez dit que le chat a ${chat.value} pattes et que la capitale de la Suisse est ${capitale.value}`,
    )
  }
}
</script>

<template>
  <form @submit="submit">
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
    <button class="btn btn-primary" :class="{ disabled: !filled }" type="submit">Terminer</button>
  </form>
  <form @submit="submit">
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
    <button class="btn btn-primary" :class="{ disabled: !filled }" type="submit">Terminer</button>
  </form>
  <form @submit="submit">
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
  </form>
</template>
