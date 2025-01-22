<template>
  <div
    id="choose-card"
    class="pointer-events-none aspect-square w-full max-w-sm rounded-md border pb-4 text-center transition-opacity duration-300"
    :class="{ 'opacity-in': choosenMember !== null }"
  >
    <figure class="overflow-hidden rounded-md p-4">
      <img
        :src="choosenMember?.image"
        :alt="`${choosenMember?.name}-profile-image`"
        class="block aspect-square max-w-full object-cover"
      />
    </figure>
    <h5>{{ choosenMember?.name }}</h5>
  </div>
</template>

<script setup lang="ts">
import type { Member } from '@/static/type'

defineProps<{
  choosenMember: Member | null
}>()
</script>

<style scoped>
.opacity-in {
  animation: opacity-active 0.6s ease-in-out alternate;
}
@keyframes opacity-active {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}
</style>
