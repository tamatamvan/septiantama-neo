<script lang="ts">
import { defineComponent, PropType } from '@nuxtjs/composition-api'

type CursorItem = {
  title: string
  slug: string
}

type CursorItems = CursorItem[]

export default defineComponent({
  props: {
    cursor: {
      type: Array as PropType<CursorItems>,
      default: [],
    },
  },
})
</script>
<template>
  <div v-if="cursor.length > 0" class="cursor w-full flex mt-4">
    <div class="prev w-1/2">
      <nuxt-link
        v-if="cursor[0]"
        :to="`/unspokens/${cursor[0].slug}`"
        class="flex items-center"
      >
        <IconWrapper class="mr-2">
          <ChevronLeftDouble />
        </IconWrapper>
        {{ cursor[0].title }}
      </nuxt-link>
    </div>
    <div class="next w-1/2">
      <nuxt-link
        v-if="cursor[1]"
        :to="`/unspokens/${cursor[1].slug}`"
        class="flex items-center justify-end text-right"
      >
        {{ cursor[1].title }}
        <IconWrapper class="ml-2">
          <ChevronRightDouble />
        </IconWrapper>
      </nuxt-link>
    </div>
  </div>
</template>
