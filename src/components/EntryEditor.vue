<script lang="ts" setup>
import EmojiField from "@/components/EmojiField.vue"
import ArrowCircleRight from "@/assets/icons/arrow-circle-right.svg?component"
import { computed, onMounted, ref, inject } from "vue"
import type { Emoji } from "@/types/Emoji"
import type { Entry } from "@/types/Entry"
import { userInjectionKey } from "@/injectionKeys"

const textMaxLength = 280
const text = ref("")

const emoji = ref<Emoji | null>(null)
// emoji.value = "crying"
// Editor should only allow you to use the Emojis from the Emoji type

const injectedUser = inject(userInjectionKey)

const charCount = computed(() => text.value.length)

// Template refs
const textarea = ref<HTMLTextAreaElement | null>(null)
onMounted(() => textarea.value?.focus())

// In this case we don't need to explictly set the type
// As it is very straighforward and would be redundant
// (length ALWAYS returns a number)
// const charCount = computed<number>(() => text.value.length)

// defineEmits(["create"])
const emit = defineEmits<{
  (e: "@create", entry: Entry): void
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

function handleSubmit() {
  emit("@create", {
    body: text.value,
    emoji: emoji.value,
    createdAt: new Date(),
    userId: injectedUser?.id || 0,
    id: Math.random(),
  })
  text.value = ""
  emoji.value = null
}
</script>
<template>
  <form class="entry-form" @submit.prevent="handleSubmit">
    <textarea
      ref="textarea"
      :value="text"
      :placeholder="`New Journal Entry for ${injectedUser?.username}`"
      @keyup="handleTextInput"
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
