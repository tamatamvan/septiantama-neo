<script>
// import format from 'date-fns/format'
import PageTitle from '../../components/commons/PageTitle'
export default {
  components: {
    PageTitle,
  },
  async asyncData({ $content }) {
    const articles = await $content('unspokens').fetch()

    return {
      articles,
    }
  },
}
</script>

<template>
  <div class="unspokens w-1/2 ml-auto mr-auto">
    <PageTitle title="Unspoken Words" />
  </div>
</template>
