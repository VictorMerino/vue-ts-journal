<script lang="ts" setup>
import EmojiField from "@/components/EmojiField.vue"
import ArrowCircleRight from "@/assets/icons/arrow-circle-right.svg"
import { computed, ref } from "vue"
import type { Emoji } from "@/types/Emoji"

const textMaxLength = 280
const text = ref("")

const emoji = ref<Emoji | null>(null)
// emoji.value = "crying"
// Editor should only allow you to use the Emojis from the Emoji type

const charCount = computed(() => text.value.length)
// In this case we don't need to explictly set the type
// As it is very straighforward and would be redundant
// (length ALWAYS returns a number)
// const charCount = computed<number>(() => text.value.length)

// defineEmits(["create"])
defineEmits<{
  (e: "@create", entry: { text: string; emoji: Emoji | null }): void
}>()
/**
 * Handy defineEmits snippet:
 * https://gist.github.com/danielkellyio/773d37ccc89ba069d650dcca09b402a1
 */

function handleTextInput(e: Event) {
  const textarea = e.target as HTMLTextAreaElement

  const textAreaValue = textarea.value
  if (textAreaValue.length <= textMaxLength) {
    return (text.value = textAreaValue)
  }
  return (text.value = textarea.value =
    textAreaValue.substring(0, textMaxLength))
}
</script>
<template>
  <form class="entry-form" @submit.prevent="$emit('@create', { text, emoji })">
    <textarea
      :value="text"
      @keyup="handleTextInput"
      placeholder="New Journal Entry for danielkelly_io"
    ></textarea>
    <EmojiField v-model="emoji" />
    <div class="entry-form-footer">
      <span :style="{ color: charCount === textMaxLength ? 'red' : 'inherit' }">
        {{ charCount }} / {{ textMaxLength }}
      </span>
      <button>Remember <ArrowCircleRight width="20" /></button>
    </div>
  </form>
</template>
