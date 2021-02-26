<script lang="ts">
import { defineComponent, computed, PropType } from '@nuxtjs/composition-api'

type BorderStyleT = 'solid' | 'dashed' | 'double' | 'dotted' | 'none'

interface BorderClassParams {
  x: 'left' | 'right'
  y: 'top' | 'bottom'
  width: number
  color: string
  style: BorderStyleT
}

export default defineComponent({
  props: {
    size: {
      type: Number,
      default: 12,
    },
    width: {
      type: Number,
      default: 2,
    },
    color: {
      type: String,
      default: 'white',
    },
    borderStyle: {
      type: String as PropType<BorderStyleT>,
      default: 'solid',
    },
  },
  setup(props) {
    const { size } = props
    const sizeClass = computed(() => `w-${size} h-${size}`)
    const borderClassParams = {
      width: props.width,
      color: props.color,
      style: props.borderStyle,
    }
    const generateBorderClass = ({
      x,
      y,
      width,
      color,
      style,
    }: BorderClassParams) => {
      const xInitial = x[0]
      const yInitial = y[0]
      return `absolute ${x}-0 ${y}-0 border-${xInitial}-${width} border-${yInitial}-${width} border-${color} border-${style}`
    }
    const borderClass = computed(() => ({
      topLeft: generateBorderClass({
        ...borderClassParams,
        x: 'left',
        y: 'top',
      }),
      topRight: generateBorderClass({
        ...borderClassParams,
        x: 'right',
        y: 'top',
      }),
      bottomLeft: generateBorderClass({
        ...borderClassParams,
        x: 'left',
        y: 'bottom',
      }),
      bottomRight: generateBorderClass({
        ...borderClassParams,
        x: 'right',
        y: 'bottom',
      }),
    }))

    return {
      sizeClass,
      borderClass,
    }
  },
})
</script>

<template>
  <div class="corner-bordered relative w-full h-full">
    <div :class="`${borderClass.topLeft} ${sizeClass}`"></div>
    <div :class="`${borderClass.topRight} ${sizeClass}`"></div>
    <div :class="`${borderClass.bottomLeft} ${sizeClass}`"></div>
    <div :class="`${borderClass.bottomRight} ${sizeClass}`"></div>
    <slot />
  </div>
</template>
