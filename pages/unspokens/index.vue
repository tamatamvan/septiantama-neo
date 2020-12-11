<script>
import format from 'date-fns/format'
import { defineComponent, useContext, useAsync } from '@nuxtjs/composition-api'
import PageTitle from '../../components/commons/PageTitle'

export default defineComponent({
  components: {
    PageTitle,
  },
  setup() {
    const { $content } = useContext()
    const articles = useAsync(
      async () =>
        await $content('unspokens')
          .only(['title', 'date', 'description', 'slug'])
          .sortBy('createdAt', 'desc')
          .fetch()
    )

    return {
      format,
      articles,
    }
  },
})
</script>

<template>
  <div class="unspokens w-1/2 ml-auto mr-auto">
    <PageTitle title="Unspoken Words" />
    <nuxt-link
      v-for="article in articles"
      :key="`article-${article.slug}`"
      :to="`/unspokens/${article.slug}`"
      class="article-item block mb-16"
    >
      <h3 class="article-item-title text-xl font-bold pb-2">
        {{ article.title }}
      </h3>
      <div class="article-item-info text-sm pb-2">
        Published at:
        {{ format(new Date(article.date), 'LLL do, yyyy - h:mm bbbb') }}
      </div>
      <p class="article-item-summary">
        {{ article.description }}
      </p>
    </nuxt-link>
  </div>
</template>
