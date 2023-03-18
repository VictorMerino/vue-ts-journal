<script setup lang="ts">
import { reactive } from "vue"

import TheHeader from "@/components/TheHeader.vue"
import EntryEditor from "./components/EntryEditor.vue"
import EntryCard from "@/components/EntryCard.vue"

import type { User } from "./types/User"

const sum = (x: number) => x * 2
sum(2)

const user: User = reactive({
  id: 1,
  username: "Davol",
  settings: [] as string[],
})

console.log(user.id)

function entryCreated(e) {
  console.log(e)
}
</script>

<template>
  <main class="container m-auto p-10">
    {{ user.username }}
    <TheHeader />
    <EntryEditor @@create="entryCreated" />
    <ul>
      <li>
        <EntryCard />
      </li>
    </ul>
  </main>
</template>
