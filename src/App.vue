<script setup lang="ts">
import { ref } from 'vue'
import { members } from '@/static/data'

const selectedMembers = ref([members[0], members[1]])
const index = ref<number>(1)
const isFinished = ref<boolean>(false)
const choosenMember = ref<string | undefined>(undefined)

const getChoose = (choose: string) => {
  const unChooseMember = members.filter((c) => !c.name.includes(choose))

  console.log(index.value)
  console.log(members.length - 1)
  choosenMember.value = choose

  if (index.value === members.length - 1) {
    alert('Ur choose are finished ' + choose)
    isFinished.value = true
    return
  }

  if (selectedMembers.value[0].name === choose) {
    selectedMembers.value[1] = unChooseMember[index.value]
  } else if (selectedMembers.value[1].name === choose) {
    selectedMembers.value[0] = unChooseMember[index.value]
  } else return

  index.value++
}

const reset = () => {
  index.value = 1
  selectedMembers.value = [members[0], members[1]]
  isFinished.value = false
  choosenMember.value = undefined
  return
}
</script>

<template>
  <header id="container-all">
    <h1 class="font-sans text-4xl">This <span class="text-xl">or</span> That</h1>
  </header>

  <main>
    <section class="mt-14 grid w-full gap-10 sm:grid-cols-2">
      <ul id="choose-wrapper" v-for="member in selectedMembers" :key="member.name">
        <li
          id="choose-card"
          class="aspect-square w-full cursor-pointer rounded-md border pb-4 text-center transition-all duration-300 hover:shadow-md"
          @click="getChoose(member.name)"
          :class="{
            'pointer-events-none opacity-80': isFinished,
            'border-4 border-green-400': choosenMember === member.name,
          }"
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
    </section>

    <button
      @click="reset"
      class="mx-auto mt-10 block rounded-lg bg-blue-700 px-5 py-2.5 text-sm font-medium text-white hover:bg-blue-800 focus:ring-4 focus:ring-blue-300"
    >
      Reset
    </button>
  </main>
</template>

<style scoped>
:global(#app) {
  @apply mx-auto flex min-h-screen max-w-2xl flex-col items-center justify-center p-4;
}
</style>
