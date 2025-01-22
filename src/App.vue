<script setup lang="ts">
import { ref } from 'vue'
import { members } from '@/static/data'
import type { Member } from '@/static/type'
import MemberList from '@/components/ui/MemberList.vue'
import PickedMemberCard from '@/components/ui/PickedMemberCard.vue'
import ButtonItem from '@/components/ui/ButtonItem.vue'
import HeaderItem from '@/components/ui/HeaderItem.vue'

const selectedMembers = ref([members[0], members[1]])
const index = ref<number>(1)
const isFinished = ref<boolean>(false)
const choosenMember = ref<Member | null>(null)

const getChoose = (choose: string) => {
  const unChooseMember = members.filter((member) => !member.name.includes(choose))

  const finalMember = members.find((member) => member.name === choose)
  if (finalMember) choosenMember.value = finalMember

  if (index.value === members.length - 1) isFinished.value = true

  if (selectedMembers.value[0].name === choose)
    selectedMembers.value[1] = unChooseMember[index.value]
  else if (selectedMembers.value[1].name === choose)
    selectedMembers.value[0] = unChooseMember[index.value]
  else return

  index.value++
}

const reset = () => {
  index.value = 1
  selectedMembers.value = [members[0], members[1]]
  isFinished.value = false
  choosenMember.value = null
}
</script>

<template>
  <header class="space-y-2">
    <header-item :is-finished />
  </header>

  <main>
    <section class="mt-10">
      <member-list
        v-if="!isFinished"
        :selected-members
        :is-finished
        :choosen-member
        @get-choose="getChoose"
      />
      <picked-member-card v-else :choosen-member />
    </section>

    <button-item :choosen-member @reset="reset" />
  </main>
</template>

<style scoped>
:global(#app) {
  @apply mx-auto flex min-h-screen max-w-2xl flex-col items-center justify-center p-4;
}
</style>
