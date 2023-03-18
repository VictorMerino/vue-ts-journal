<script setup lang="ts">
import { reactive } from "vue"

import TheHeader from "@/components/TheHeader.vue"
import EntryEditor from "./components/EntryEditor.vue"
import EntryCard from "@/components/EntryCard.vue"

import type { User } from "./types/User"
import type { Entry } from "./types/Entry"

const sum = (x: number) => x * 2
sum(2)

const user: User = reactive({
  id: 1,
  username: "Davol",
  settings: [] as string[],
})

console.log(user.id)

function handleCreateEntry(entry: Entry) {
  console.log(entry)
}
</script>

<template>
  <main class="container m-auto p-10">
    {{ user.username }}
    <TheHeader />
    <EntryEditor @@create="handleCreateEntry" />
    <ul>
      <li>
        <EntryCard />
      </li>
    </ul>
  </main>
</template>
