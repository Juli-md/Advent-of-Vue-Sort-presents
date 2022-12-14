<template>
  <div class="w-full h-full p-4 flex justify-center items-center">
    <div class="max-w-md">
      <div>
        <img src="/assets/tree.svg" alt="Christmas tree" />
      </div>
      <div class="mt-2 flex justify-center items-center" v-if="applySorting">
        <img
          v-for="present in presentsSorted"
          :key="present.id"
          :src="present.src"
          :alt="`Present ${present.id}`"
          data-qa="present"
        />
      </div>
      <div class="mt-2 flex justify-center items-center" v-if="!applySorting">
        <img
          v-for="present in presents"
          :key="present.id"
          :src="present.src"
          :alt="`Present ${present.id}`"
          data-qa="present"
        />
      </div>
      <button
        @click="applySorting = !applySorting"
        class="block w-24 h-8 mx-auto mt-6 text-white font-semibold bg-indigo-500 rounded"
      >
        Toggle sort
      </button>
    </div>
  </div>
</template>

<script setup>
import presents from './presents.json'
import { ref, computed } from 'vue'
let applySorting = ref(false)
const presentsSorted = computed(() => {
  const sortedPresents = [...presents].sort((a, b) =>
    a.dimensions.width * a.dimensions.height > b.dimensions.width * b.dimensions.height ? 1 : -1
  )
  return sortedPresents
})
</script>
