<template>
  <button
    @click="handleReset"
    :disabled="isDisabled"
    :class="disabledClass"
    class="mx-auto mt-10 block rounded-lg bg-blue-700 px-5 py-2.5 text-sm font-medium text-white hover:bg-blue-800 focus:ring-4 focus:ring-blue-300"
  >
    Reset
  </button>
</template>

<script setup lang="ts">
import type { Member } from '@/static/type'
import { computed } from 'vue'

const props = defineProps<{
  choosenMember: Member | null
}>()
const isDisabled = computed(() => props.choosenMember === null)
const disabledClass = computed(() => isDisabled.value && 'pointer-events-none opacity-50')

const emit = defineEmits<{ (event: 'reset'): void }>()
const handleReset = () => emit('reset')
</script>
