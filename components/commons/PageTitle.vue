<script lang="ts">
import { defineComponent } from '@nuxtjs/composition-api'
import LineHeading from './LineHeading.vue'

export default defineComponent({
  props: {
    title: String,
  },
  components: {
    LineHeading,
  },
})
</script>

<template>
  <div class="pt-8 pb-12">
    <LineHeading>
      <h1 class="text-3xl font-bold">{{ title }}</h1>
    </LineHeading>
  </div>
</template>
