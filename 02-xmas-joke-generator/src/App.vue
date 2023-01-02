<template>
  <div class="w-full h-full flex justify-center items-center">
    <div v-if="isLoading">
      Loading...
    </div>
    <div class="max-w-xs w-full flex flex-col" v-else>
      <p class="w-3/4 p-4 rounded-2xl bg-slate-400 text-white self-start">{{ jokeQuestion }}</p>
      <p class="w-3/4 mt-2 p-4 rounded-2xl bg-orange-500 text-white self-end" v-if="isbtnNextSeen">{{ jokeAnswer }}</p>

      <div class="my-4 flex justify-center items-center">
        <button class="bg-emerald-400 px-8 py-3 rounded-lg hover:opacity-75" v-if="isbtnNextSeen" @click="getJokes">😂
          Next
          joke</button>
        <button class="bg-emerald-400 px-8 py-3 rounded-lg hover:opacity-75" v-else @click="showJoke">Tell
          me!</button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const jokeQuestion = ref('')
const jokeAnswer = ref('')
let isbtnNextSeen = ref(false)
let isLoading = ref(true)

const getJokes = async () => {
  isbtnNextSeen.value = false
  isLoading.value = true
  jokeQuestion.value = ''
  jokeAnswer.value = ''

  try {
    const response = await fetch(`https://v2.jokeapi.dev/joke/christmas`).then(response => response.json())
    jokeQuestion.value = response.setup
    jokeAnswer.value = response.delivery
    isLoading.value = false
  } catch (error) {
    console.log(error)
    alert('There is Error!')
  }

}
getJokes()

function showJoke() {
  isbtnNextSeen.value = true
}

</script>
