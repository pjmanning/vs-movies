<template>
  <div class="observer" />
</template>

<script lang="ts">
import { defineComponent, onMounted, onUnmounted } from 'vue'

export default defineComponent({
  name: 'IntersectionObserver',
  props: {
    options: {
      type: Object,
      default: () => ({}),
    },
  },
  setup(props, { emit }) {
    let observer: IntersectionObserver | null = null

    onMounted(() => {
      observer = new IntersectionObserver(([entry]) => {
        if (entry && entry.isIntersecting) {
          emit('intersect')
        }
      }, props.options)

      observer.observe(document.querySelector('.observer')!)
    })

    onUnmounted(() => {
      if (observer) {
        observer.disconnect()
      }
    })

    return {}
  },
})
</script>
