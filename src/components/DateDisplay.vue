<script lang="ts">
import formatRelative from "date-fns/formatRelative"
import { defineComponent /* , type PropType */ } from "vue"
// import type { Entry } from "@/types/Entry"
export default defineComponent({
  props: {
    date: { type: Date, required: true },
    // This would be the way to type props in Options API:
    // date: { type: Object as PropType<Entry>, required: true },
  },
  // Typing emit events is bloody easy, just like a normal function:
  /* emits: {
    emitSomething(payload: Entry) {
      return payload.body && payload.createdAt
    },
  }, */
  computed: {
    formatted() /* : string */ {
      return formatRelative(this.date, Date.now())
    },
  },
  mounted() {
    this.formatted
  },
})
</script>
<template>
  <div>{{ formatted }}</div>
</template>
