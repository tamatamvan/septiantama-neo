<script>
import format from 'date-fns/format'
export default {
  async asyncData({ $content, params }) {
    const article = await $content('unspokens', params.slug).fetch()

    return {
      article: {
        ...article,
        publisedDate: format(new Date(article.date), 'LLL Do, yyyy - h:m bbbb'),
      },
    }
  },
}
</script>

<style scoped>
* {
  font-family: 'Merriweather', serif;
}
</style>

<style>
.nuxt-content p {
  margin-bottom: 1.5em;
}
.nuxt-content hr {
  background-image: linear-gradient(
    to right,
    rgba(0, 0, 0, 0),
    rgb(25, 118, 210, 0.8),
    rgba(0, 0, 0, 0)
  );
  border: 0;
  height: 2px;
  margin: 32px auto;
}
</style>

<template>
  <article class="flex flex-wrap">
    <div class="h-screen w-full md:fixed md:left-0 md:w-1/2">
      <img
        src="/unspoken.jpeg"
        :alt="article.title"
        class="poem-img h-screen w-full object-cover object-center"
      />
    </div>
    <div
      class="article-header h-screen w-full absolute text-center md:fixed md:left-0 md:w-1/2 p-16 md:p-32 bg-black bg-opacity-75"
    >
      <div
        class="flex flex-col justify-center items-center h-full w-full text-white"
      >
        <h1 class="article-title text-2xl md:text-3xl italic bold">
          {{ article.title }}
        </h1>
        <br />
        <p>
          Published at:
          <span class="block">{{ article.publisedDate }}</span>
        </p>
      </div>
    </div>
    <div
      class="min-h-screen w-full md:w-1/2 md:ml-auto justify-self-end p-16 lg:p-32 flex items-center justify-center"
    >
      <nuxt-content :document="article" />
    </div>
  </article>
</template>
