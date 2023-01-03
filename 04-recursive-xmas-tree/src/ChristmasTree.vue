<template>
  <div>
    <div v-for="i in size" class="flex justify-center">
      <div v-for="j in i" class="relative rounded-full bg-green w-16 h-16 -m-2 flex justify-center items-center" />
    </div>
  </div>
</template>

<script setup lang="ts">
withDefaults(
  defineProps<{
    size: number
  }>(),
  {
    size: 1,
  }
)
</script>
