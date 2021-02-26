<script lang="ts">
import { defineComponent } from '@nuxtjs/composition-api'
import CornerBorder from '~/components/candies/CornerBorder.vue'

export default defineComponent({
  components: { CornerBorder },
})
</script>
<template>
  <div class="homepage">
    <div class="header">
      <div class="container mx-auto w-screen h-screen py-16">
        <CornerBorder>
          <div
            class="header-content h-full w-full flex items-center justify-center"
          >
            <h1 class="text-white text-6xl tracking-in-expand">SEPTIAN TAMA</h1>
          </div>
        </CornerBorder>
      </div>
    </div>
  </div>
</template>

<style lang="scss" scoped>
.header {
  background-color: #1b262c;

  /* &-content {
    border: solid 3px #fff;
  } */
}
.tracking-in-expand {
  animation: tracking-in-expand 1s cubic-bezier(0.215, 0.61, 0.355, 1) both;
}
@keyframes tracking-in-expand {
  0% {
    letter-spacing: -0.5em;
    opacity: 0;
  }
  40% {
    opacity: 0.6;
  }
  100% {
    opacity: 1;
  }
}
</style>
