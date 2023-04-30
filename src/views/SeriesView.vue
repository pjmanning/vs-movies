<script setup lang="ts">
import { ref, onErrorCaptured } from 'vue'
import type { Ref } from 'vue'
import InfiniteScroll from '@/components/InfiniteScroll.vue'
import Loading from '@/components/Loading.vue'

const error: Ref<Error | null> = ref(null)
onErrorCaptured((e) => {
  error.value = e
})
</script>

<template>
  <div>
    <div v-if="error">{{ error }}</div>
    <Suspense>
      <InfiniteScroll />

      <template #fallback>
        <Loading class="mt-44 h-20 w-20" />
      </template>
    </Suspense>
  </div>
</template>

<style scoped></style>
