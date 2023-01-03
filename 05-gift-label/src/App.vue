<template>
  <div class="w-full h-full flex justify-center items-center">
    <div>
      <form class="mb-4">
        <fieldset class="mb-3">
          <label for="gift-to" class="block text-sm font-medium text-slate-700">To: </label>
          <input type="text" id="gift-to" name="gift-to" v-model="giftTo"
            class="w-full mt-1 bg-white rounded-md px-3 py-2 border border-slate-300">
        </fieldset>

        <fieldset class="mb-3">
          <label for="gift-from" class="block text-sm font-medium text-slate-700">From: </label>
          <input type="text" id="gift-from" name="gift-from" v-model="giftFrom"
            class="w-full mt-1 bg-white rounded-md px-3 py-2 border border-slate-300">
        </fieldset>
      </form>

      <div class="w-full max-w-2xl p-4 rounded bg-red-400 text-white">
        <div class="border-2 rounded flex flex-col md:flex-row md:items-center md:gap-8 p-4">
          <img src="/assets/santa.svg" alt="" class="max-w-[12em]" />
          <div>
            <h1 class="font-serif text-4xl">Happy Holidays!</h1>
            <div class="mt-4 bg-white text-black p-2 rounded">TO: {{ giftTo }}</div>
            <div class="mt-2 bg-white text-black p-2 rounded">FROM: {{ giftFrom }}</div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const giftTo = ref('')
const giftFrom = ref('')

</script>
