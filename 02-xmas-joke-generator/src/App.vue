<template>
  <div class="w-full h-full flex justify-center items-center">
    <!-- <span class="text-3xl">Good luck!</span> -->
    <div class="flex flex-col">
      <p class="text-2xl">{{ jokeQuestion }}</p>
      <p class="text-1xl" v-if="isJokeAnswerSeen">{{ jokeAnswer }}</p>
      <button class="bg-green px-8 py-3 rounded-lg hover:opacity-75" v-if="isbtnTellMeSeen" @click="showJokeAns">Tell
        me!</button>
      <button class="bg-green px-8 py-3 rounded-lg hover:opacity-75" v-if="isbtnNextSeen" @click="getNextJoke">😂 Next
        joke</button>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const jokeQuestion = ref('')
const jokeAnswer = ref('')
let isJokeAnswerSeen = ref(false)
let isbtnTellMeSeen = ref(true)
let isbtnNextSeen = ref(false)

const getJokes = async () => {
  const response = await fetch(`https://v2.jokeapi.dev/joke/christmas`)
  const data = await response.json()
  jokeQuestion.value = data.setup
  jokeAnswer.value = data.delivery
}
getJokes()

function showJokeAns() {
  console.log('Button clicked!')
  isJokeAnswerSeen.value = true
  isbtnTellMeSeen.value = false
  isbtnNextSeen.value = true
}

function getNextJoke() {
  isJokeAnswerSeen.value = false
  isbtnTellMeSeen.value = true
  isbtnNextSeen.value = false
  getJokes()
}
</script>
