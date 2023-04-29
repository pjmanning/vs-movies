<script setup lang="ts">
import { ref } from 'vue'
import { RouterLink } from 'vue-router'
import { Dialog, DialogPanel, TransitionChild, TransitionRoot } from '@headlessui/vue'
import { FilmIcon, HomeIcon, TvIcon, XMarkIcon } from '@heroicons/vue/24/outline'
import { MagnifyingGlassIcon } from '@heroicons/vue/20/solid'
import { VideoCameraIcon } from '@heroicons/vue/24/solid'
import TheHeader from './components/TheHeader.vue'

const navigation = [
  { name: 'Home', url: '/', icon: HomeIcon },
  { name: 'Movies', url: '/movies', icon: FilmIcon },
  { name: 'Series', url: '/series', icon: TvIcon },
  { name: 'Search', url: '/search', icon: MagnifyingGlassIcon },
]

const mobileMenuOpen = ref(false)
</script>

<template>
  <div class="flex h-full">
    <!-- Narrow sidebar -->
    <div class="hidden w-28 overflow-y-auto bg-slate-900 md:block">
      <div class="flex w-full flex-col items-center py-6">
        <RouterLink to="/" class="flex flex-shrink-0 items-center">
          <VideoCameraIcon class="h-8 w-auto text-white" />
        </RouterLink>
        <div class="mt-6 w-full flex-1 space-y-1 px-2">
          <RouterLink v-for="item in navigation" :key="item.name" :to="item.url" class="nav-links group flex w-full flex-col items-center rounded-md p-3 text-xs font-medium text-slate-100 hover:bg-slate-800 hover:text-white">
            <component :is="item.icon" class="h-6 w-6 text-slate-300 group-hover:text-white" aria-hidden="true" />
            <span class="mt-2">{{ item.name }}</span>
          </RouterLink>
        </div>
      </div>
    </div>

    <!-- Mobile menu -->
    <TransitionRoot as="template" :show="mobileMenuOpen">
      <Dialog as="div" class="relative z-40 md:hidden" @close="mobileMenuOpen = false">
        <TransitionChild as="template" enter="transition-opacity ease-linear duration-300" enter-from="opacity-0" enter-to="opacity-100" leave="transition-opacity ease-linear duration-300" leave-from="opacity-100" leave-to="opacity-0">
          <div class="fixed inset-0 bg-gray-600 bg-opacity-75" />
        </TransitionChild>

        <div class="fixed inset-0 z-40 flex">
          <TransitionChild as="template" enter="transition ease-in-out duration-300 transform" enter-from="-translate-x-full" enter-to="translate-x-0" leave="transition ease-in-out duration-300 transform" leave-from="translate-x-0" leave-to="-translate-x-full">
            <DialogPanel class="relative flex w-full max-w-xs flex-1 flex-col bg-slate-700 pb-4 pt-5">
              <TransitionChild as="template" enter="ease-in-out duration-300" enter-from="opacity-0" enter-to="opacity-100" leave="ease-in-out duration-300" leave-from="opacity-100" leave-to="opacity-0">
                <div class="absolute right-0 top-1 -mr-14 p-1">
                  <button type="button" class="flex h-12 w-12 items-center justify-center rounded-full focus:outline-none focus:ring-2 focus:ring-white" @click="mobileMenuOpen = false">
                    <XMarkIcon class="h-6 w-6 text-white" aria-hidden="true" />
                    <span class="sr-only">Close sidebar</span>
                  </button>
                </div>
              </TransitionChild>
              <div class="flex flex-shrink-0 items-center px-4">
                <VideoCameraIcon class="h-8 w-auto text-white" />
              </div>
              <div class="mt-5 h-0 flex-1 overflow-y-auto px-2">
                <nav class="flex h-full flex-col">
                  <div class="space-y-1">
                    <RouterLink v-for="item in navigation" :key="item.name" :to="item.url" class="nav-links font-medium'] group flex items-center rounded-md px-3 py-2 text-sm text-slate-100 hover:bg-slate-800 hover:text-white">
                      <component :is="item.icon" class="mr-3 h-6 w-6 text-slate-300 group-hover:text-white" aria-hidden="true" />
                      <span>{{ item.name }}</span>
                    </RouterLink>
                  </div>
                </nav>
              </div>
            </DialogPanel>
          </TransitionChild>
          <div class="w-14 flex-shrink-0" aria-hidden="true">
            <!-- Dummy element to force sidebar to shrink to fit close icon -->
          </div>
        </div>
      </Dialog>
    </TransitionRoot>

    <!-- Content area -->
    <div class="flex min-h-screen flex-1 flex-col overflow-hidden">
      <TheHeader />
      <RouterView />
    </div>
  </div>
</template>

<style scoped>
.nav-links.router-link-active.router-link-exact-active {
  @apply bg-slate-800 text-white;
}
</style>
