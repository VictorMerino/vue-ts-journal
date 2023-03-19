<script setup lang="ts">
import { computed, reactive, provide } from "vue"

import TheHeader from "@/components/TheHeader.vue"
import EntryEditor from "./components/EntryEditor.vue"
import EntryCard from "@/components/EntryCard.vue"

import type { User } from "./types/User"
import type { Entry } from "./types/Entry"

import { userInjectionKey } from "./injectionKeys"

const sum = (x: number) => x * 2
sum(2)

const user: User = reactive({
  id: 1,
  userName: "Davol",
  settings: [] as string[],
})
provide(userInjectionKey, user)

const entries = reactive<Entry[]>([])
const entriesReversed = computed(() => [...entries].reverse())
console.log(user.id)

function handleCreateEntry(entry: Entry) {
  entries.push(entry)
}
</script>

<template>
  <main class="container m-auto p-10">
    {{ user.userName }}
    <TheHeader />
    <EntryEditor @@create="handleCreateEntry" />
    <ul>
      <li v-for="entry in entriesReversed" :key="entry.id">
        <EntryCard :entry="entry" />
      </li>
      <li></li>
    </ul>
  </main>
</template>
