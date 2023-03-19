<script lang="ts" setup>
import DateDisplay from "./DateDisplay.vue"
import UseEmojis from "@/composables/UseEmojis"
import type { Entry } from "@/types/Entry"
const { findEmoji } = UseEmojis()

// This is the non-TS way of declaring a prop:
/* defineProps({
  entry: { type: Object, default: () => ({}) },
}) */

// And this is the TS way:
defineProps<{ entry: Entry }>()
</script>
<template>
  <div class="entry-card">
    <div class="entry-card-body">
      <component :is="findEmoji(entry.emoji)" width="75"></component>
      <div class="entry-text">{{ entry.body }}</div>
    </div>
    <div class="entry-footer">
      <DateDisplay :date="entry.createdAt" class="mr-2" />
      |
      <span class="ml-2">{{ entry.userId }}</span>
    </div>
  </div>
</template>
