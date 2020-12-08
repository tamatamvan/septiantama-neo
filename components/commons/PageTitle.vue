<script lang="ts">
import { defineComponent } from '@nuxtjs/composition-api'

export default defineComponent({
  props: {
    title: String,
  },
})
</script>

<template>
  <h1 class="text-3xl font-bold pt-8 pb-12">{{ title }}</h1>
</template>
