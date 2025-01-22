<template>
  <h1 class="text-center font-sans text-4xl font-semibold">
    This <span class="text-xl">or</span> That
  </h1>
  <p class="text-center">
    {{ isFinishedText }}
  </p>
</template>

<script setup lang="ts">
import { computed } from 'vue'

const props = defineProps<{
  isFinished: boolean
}>()

const isFinishedText = computed(() =>
  props.isFinished
    ? 'Your final choice is'
    : 'Choose between two options by clicking on the image.',
)
</script>
