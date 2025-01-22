<template>
  <div class="grid w-full grid-cols-2 gap-10" v-auto-animate>
    <ul id="choose-wrapper" v-for="member in selectedMembers" :key="member.name">
      <li
        id="choose-card"
        class="aspect-square w-full cursor-pointer rounded-md border pb-4 text-center transition-all duration-300 hover:shadow-md"
        @click="handleClick(member)"
        :class="handledClasses(member)"
      >
        <figure class="overflow-hidden rounded-md p-4">
          <img
            :src="member.image"
            :alt="`${member.name}-profile-image`"
            class="block aspect-square max-w-full object-cover"
          />
        </figure>
        <h5>{{ member.name }}</h5>
      </li>
    </ul>
  </div>
</template>

<script setup lang="ts">
import type { Member } from '@/static/type'

const props = defineProps<{
  selectedMembers: Member[]
  isFinished: boolean
  choosenMember: Member | null
}>()

const handledClasses = (member: Member) => ({
  'pointer-events-none opacity-80': props.isFinished,
  'border-4 border-green-400': props.choosenMember?.name === member.name,
})

const emit = defineEmits<{
  (event: 'get-choose', value: string): void
}>()
const handleClick = (member: Member) => emit('get-choose', member.name)
</script>
