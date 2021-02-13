<script lang="ts">
import { defineComponent, useAsync, useContext } from '@nuxtjs/composition-api'
import format from 'date-fns/format'

import ChevronLeftDouble from '~/components/icons/ChevronLeftDouble.vue'
import ChevronRightDouble from '~/components/icons/ChevronRightDouble.vue'
import IconWrapper from '~/components/commons/IconWrapper.vue'
import LineHeading from '~/components/commons/LineHeading.vue'
import PrevNextNav from '~/components/commons/PrevNextNav.vue'

export default defineComponent({
  setup() {
    const { $content, params } = useContext()
    const article = useAsync(
      async () => await $content('unspokens', params.value.slug).fetch()
    )
    const cursor = useAsync(
      async () =>
        await $content('unspokens')
          .only(['title', 'slug'])
          .sortBy('createdAt', 'asc')
          .surround(params.value.slug)
          .fetch()
    )

    return {
      article,
      cursor,
      format,
    }
  },
  components: {
    IconWrapper,
    ChevronLeftDouble,
    ChevronRightDouble,
    LineHeading,
    PrevNextNav,
  },
})
</script>

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
        :alt="article && article.title"
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
          {{ article && article.title }}
        </h1>
        <br />
        <p>
          Published at:
          <span class="block">{{
            article &&
            format(new Date(article.date), 'LLL do, yyyy - h:mm bbbb')
          }}</span>
        </p>
      </div>
    </div>
    <div
      class="min-h-screen w-full md:w-1/2 md:ml-auto p-16 lg:p-32 flex flex-col items-center justify-center"
    >
      <nuxt-content :document="article" />
      <div class="other-pieces w-full">
        <LineHeading>
          <h4 class="text-xl text-center font-bold m-8">Other Pieces</h4>
        </LineHeading>
        <PrevNextNav :cursor="cursor" />
      </div>
    </div>
  </article>
</template>
