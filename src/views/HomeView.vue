<script setup lang="ts">
import { HeartIcon } from '@heroicons/vue/24/outline'
import { Bars4Icon, PencilIcon, PlusIcon, Squares2X2Icon as Squares2X2IconMini } from '@heroicons/vue/20/solid'
import InfiniteScroll from '@/components/InfiniteScroll.vue'

const tabs = [
  { name: 'Recently Viewed', href: '#', current: true },
  { name: 'Recently Added', href: '#', current: false },
  { name: 'Favorited', href: '#', current: false },
]
const files = [
  {
    name: 'IMG_4985.HEIC',
    size: '3.9 MB',
    source: 'https://images.unsplash.com/photo-1582053433976-25c00369fc93?ixid=MXwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=512&q=80',
    current: true,
  },
  // More files...
]
const currentFile = {
  name: 'IMG_4985.HEIC',
  size: '3.9 MB',
  source: 'https://images.unsplash.com/photo-1582053433976-25c00369fc93?ixid=MXwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=512&q=80',
  information: {
    'Uploaded by': 'Marie Culver',
    Created: 'June 8, 2020',
    'Last modified': 'June 8, 2020',
    Dimensions: '4032 x 3024',
    Resolution: '72 x 72',
  },
  sharedWith: [
    {
      id: 1,
      name: 'Aimee Douglas',
      imageUrl: 'https://images.unsplash.com/photo-1502685104226-ee32379fefbe?ixlib=rb-=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=facearea&facepad=3&w=1024&h=1024&q=80',
    },
    {
      id: 2,
      name: 'Andrea McMillan',
      imageUrl: 'https://images.unsplash.com/photo-1494790108377-be9c29b29330?ixlib=rb-1.2.1&ixqx=oilqXxSqey&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=facearea&facepad=2&w=256&h=256&q=80',
    },
  ],
}
</script>

<template>
  <div class="flex flex-1 items-stretch overflow-hidden">
    <main class="flex-1 overflow-y-auto">
      <div class="mx-auto max-w-7xl px-4 pt-8 sm:px-6 lg:px-8">
        <div class="flex">
          <h1 class="flex-1 text-2xl font-bold text-gray-900">Movies</h1>
          <div class="ml-6 flex items-center rounded-lg bg-gray-100 p-0.5 sm:hidden">
            <button type="button" class="rounded-md p-1.5 text-gray-400 hover:bg-white hover:shadow-sm focus:outline-none focus:ring-2 focus:ring-inset focus:ring-slate-500">
              <Bars4Icon class="h-5 w-5" aria-hidden="true" />
              <span class="sr-only">Use list view</span>
            </button>
            <button type="button" class="ml-0.5 rounded-md bg-white p-1.5 text-gray-400 shadow-sm focus:outline-none focus:ring-2 focus:ring-inset focus:ring-slate-500">
              <Squares2X2IconMini class="h-5 w-5" aria-hidden="true" />
              <span class="sr-only">Use grid view</span>
            </button>
          </div>
        </div>

        <!-- Tabs -->
        <div class="mt-3 sm:mt-2">
          <div class="sm:hidden">
            <label for="tabs" class="sr-only">Select a tab</label>
            <!-- Use an "onChange" listener to redirect the user to the selected tab URL. -->
            <select id="tabs" name="tabs" class="block w-full rounded-md border-0 py-1.5 pl-3 pr-10 text-gray-900 ring-1 ring-inset ring-gray-300 focus:border-slate-500 focus:ring-2 focus:ring-inset focus:ring-slate-600">
              <!-- <option selected="">Recently Viewed</option> -->
              <option>Recently Added</option>
              <option>Favorited</option>
            </select>
          </div>
          <div class="hidden sm:block">
            <div class="flex items-center border-b border-gray-200">
              <nav class="-mb-px flex flex-1 space-x-6 xl:space-x-8" aria-label="Tabs">
                <a v-for="tab in tabs" :key="tab.name" :href="tab.href" :aria-current="tab.current ? 'page' : undefined" :class="[tab.current ? 'border-slate-500 text-slate-600' : 'border-transparent text-gray-500 hover:border-gray-300 hover:text-gray-700', 'whitespace-nowrap border-b-2 px-1 py-4 text-sm font-medium']">{{ tab.name }}</a>
              </nav>
              <div class="ml-6 hidden items-center rounded-lg bg-gray-100 p-0.5 sm:flex">
                <button type="button" class="rounded-md p-1.5 text-gray-400 hover:bg-white hover:shadow-sm focus:outline-none focus:ring-2 focus:ring-inset focus:ring-slate-500">
                  <Bars4Icon class="h-5 w-5" aria-hidden="true" />
                  <span class="sr-only">Use list view</span>
                </button>
                <button type="button" class="ml-0.5 rounded-md bg-white p-1.5 text-gray-400 shadow-sm focus:outline-none focus:ring-2 focus:ring-inset focus:ring-slate-500">
                  <Squares2X2IconMini class="h-5 w-5" aria-hidden="true" />
                  <span class="sr-only">Use grid view</span>
                </button>
              </div>
            </div>
          </div>
        </div>

        <!-- Gallery -->
        <section class="mt-8 pb-16" aria-labelledby="gallery-heading">
          <h2 id="gallery-heading" class="sr-only">Recently viewed</h2>
          <InfiniteScroll />
          <!-- <ul role="list" class="grid grid-cols-2 gap-x-4 gap-y-8 sm:grid-cols-3 sm:gap-x-6 md:grid-cols-4 lg:grid-cols-3 xl:grid-cols-4 xl:gap-x-8">
            <li v-for="file in files" :key="file.name" class="relative">
              <div :class="[file.current ? 'ring-2 ring-slate-500 ring-offset-2' : 'focus-within:ring-2 focus-within:ring-slate-500 focus-within:ring-offset-2 focus-within:ring-offset-gray-100', 'group aspect-h-7 aspect-w-10 block w-full overflow-hidden rounded-lg bg-gray-100']">
                <img :src="file.source" alt="" :class="[file.current ? '' : 'group-hover:opacity-75', 'pointer-events-none object-cover']" />
                <button type="button" class="absolute inset-0 focus:outline-none">
                  <span class="sr-only">View details for {{ file.name }}</span>
                </button>
              </div>
              <p class="pointer-events-none mt-2 block truncate text-sm font-medium text-gray-900">{{ file.name }}</p>
              <p class="pointer-events-none block text-sm font-medium text-gray-500">{{ file.size }}</p>
            </li>
          </ul> -->
        </section>
      </div>
    </main>
  </div>
</template>

<style scoped></style>
