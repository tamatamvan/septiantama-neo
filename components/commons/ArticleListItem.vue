<script lang="ts">
import { computed, defineComponent, PropType } from '@nuxtjs/composition-api'
import format from 'date-fns/format'

type ArticleItem = {
  title: string
  slug: string
  date: string | number | Date
  description: string
}

export default defineComponent({
  props: {
    article: {
      type: Object as PropType<ArticleItem>,
      required: true,
    },
  },
  setup(props) {
    const publishedDate = computed(() =>
      format(new Date(props.article.date), 'LLL do, yyyy - h:mm bbbb')
    )

    return {
      publishedDate,
    }
  },
})
</script>

<template>
  <nuxt-link
    class="article-item block mb-16"
    :to="`/unspokens/${article.slug}`"
  >
    <h3 class="article-item-title text-xl font-bold pb-2">
      {{ article.title }}
    </h3>
    <div class="article-item-info text-sm pb-2">
      Published at:
      {{ publishedDate }}
    </div>
    <p class="article-item-summary">
      {{ article.description }}
    </p>
  </nuxt-link>
</template>
