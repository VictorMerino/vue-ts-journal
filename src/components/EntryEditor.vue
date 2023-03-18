<script lang="ts" setup>
import EmojiField from "@/components/EmojiField.vue"
import ArrowCircleRight from "@/assets/icons/arrow-circle-right.svg"
import { computed, ref } from "vue"
import type { Emoji } from "@/types/Emoji"

const text = ref("")

const emoji = ref<Emoji | null>(null)
// emoji.value = "crying"
// Editor should only allow you to use the Emojis from the Emoji type

const charCount = computed(() => text.value.length)
// In this case we don't need to explictly set the type
// As it is very straighforward and would be redundant
// (length ALWAYS returns a number)
// const charCount = computed<number>(() => text.value.length)
</script>
<template>
  <form class="entry-form" @submit.prevent>
    <textarea
      v-model="text"
      placeholder="New Journal Entry for danielkelly_io"
    ></textarea>
    <EmojiField v-model="emoji" />
    <div class="entry-form-footer">
      <span>{{ charCount }} / 280</span>
      <button>Remember <ArrowCircleRight width="20" /></button>
    </div>
  </form>
</template>
