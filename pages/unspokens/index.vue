<script>
import format from 'date-fns/format'
import { defineComponent, useContext, useAsync } from '@nuxtjs/composition-api'
import PageTitle from '~/components/commons/PageTitle'
import ArticleListItem from '~/components/commons/ArticleListItem'

export default defineComponent({
  components: {
    PageTitle,
    ArticleListItem,
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
    <ArticleListItem
      v-for="article in articles"
      :key="`article-${article.slug}`"
      :article="article"
    />
  </div>
</template>
