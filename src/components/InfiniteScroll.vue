<script setup lang="ts">
import { ref } from 'vue'
import type { Ref } from 'vue'
import { useInfiniteScroll } from '@vueuse/core'

interface Movie {
  Title: string
  Year: string
  imdbID: string
  Type: string
  Poster: string
}

const listEl = ref(null)
const error: Ref<Error | null> = ref(null)
const moviesList = ref<Movie[]>(await getMovies(1))
const fetchingData = ref(false)

async function getMovies(page: number) {
  try {
    console.log('get movies')
    const res = await fetch(`http://www.omdbapi.com/?s=dogs&page=${page}&apikey=f83ba545`)
    const movies = await res.json()
    return movies.Search
  } catch (e) {
    error.value = e as Error
  }
}

async function getMoviesOnScroll() {
  fetchingData.value = true
  const newMovies = await getMovies(moviesList.value.length / 10 + 1)
  fetchingData.value = false
  moviesList.value = [...moviesList.value, ...newMovies]
  console.log('get new movies')
}

useInfiniteScroll(
  listEl,
  async () => {
    await getMoviesOnScroll()
  },
  {
    distance: 100,
  }
)
</script>

<template>
  <div ref="listEl" class="-mt-16 h-screen overflow-y-auto">
    <div class="mx-auto max-w-2xl px-4 py-16 sm:px-6 sm:py-24 lg:max-w-[1600px] lg:px-8">
      <h2 class="sr-only">Movies</h2>

      <ul class="grid grid-cols-1 gap-x-6 gap-y-10 sm:grid-cols-2 lg:grid-cols-3 xl:grid-cols-5 xl:gap-x-8">
        <li v-for="movie in moviesList" :key="movie.imdbID" class="group">
          <div class="aspect-h-1 aspect-w-1 w-full overflow-hidden rounded-lg bg-gray-200 xl:aspect-h-8 xl:aspect-w-7">
            <img :src="movie.Poster" :alt="movie.Title" class="h-full w-full object-cover object-center group-hover:opacity-75" />
          </div>
          <h3 class="mt-4 text-sm text-gray-700">{{ movie.Title }}</h3>
          <p class="mt-1 text-lg font-medium text-gray-900">{{ movie.Year }}</p>
        </li>
        <p v-show="fetchingData">Fetching more movies...</p>
      </ul>
    </div>
  </div>
</template>
