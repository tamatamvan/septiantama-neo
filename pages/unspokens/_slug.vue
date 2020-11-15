<script>
import format from 'date-fns/format'
export default {
  async asyncData({ $content, params }) {
    const article = await $content('articles', params.slug).fetch()

    return {
      article: {
        ...article,
        publisedDate: format(new Date(article.date), 'LLL Do, yyyy - h:m bbbb'),
      },
    }
  },
}
</script>

<template>
  <article class="flex flex-wrap">
    <div class="h-screen w-full md:fixed md:left-0 md:w-1/2">
      <img
        src="/unspoken.jpeg"
        alt=""
        class="poem-img h-screen w-full object-cover object-center"
      />
    </div>
    <div
      class="article-header h-screen w-full md:fixed md:left-0 md:w-1/2 bg-black bg-opacity-75"
    >
      <div
        class="flex flex-col justify-center items-center h-full w-full text-white"
      >
        <h1 class="text-3xl italic">{{ article.title }}</h1>
        <br />
        <p>Published at: {{ article.publisedDate }}</p>
      </div>
    </div>
    <div
      class="min-h-screen w-full md:w-1/2 md:ml-auto justify-self-end p-16 flex items-center justify-center"
    >
      <nuxt-content :document="article" />
    </div>
  </article>
</template>
