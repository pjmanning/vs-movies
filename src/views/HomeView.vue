<script setup lang="ts">
import { ref } from 'vue'
import { Disclosure, DisclosureButton, DisclosurePanel, Menu, MenuButton, MenuItem, MenuItems } from '@headlessui/vue'
import { ChevronDownIcon, FunnelIcon, StarIcon } from '@heroicons/vue/20/solid'

const filters = {
  price: [
    { value: '0', label: '$0 - $25', checked: false },
    { value: '25', label: '$25 - $50', checked: false },
    { value: '50', label: '$50 - $75', checked: false },
    { value: '75', label: '$75+', checked: false },
  ],
  color: [
    { value: 'white', label: 'White', checked: false },
    { value: 'beige', label: 'Beige', checked: false },
    { value: 'blue', label: 'Blue', checked: true },
    { value: 'brown', label: 'Brown', checked: false },
    { value: 'green', label: 'Green', checked: false },
    { value: 'purple', label: 'Purple', checked: false },
  ],
  size: [
    { value: 'xs', label: 'XS', checked: false },
    { value: 's', label: 'S', checked: true },
    { value: 'm', label: 'M', checked: false },
    { value: 'l', label: 'L', checked: false },
    { value: 'xl', label: 'XL', checked: false },
    { value: '2xl', label: '2XL', checked: false },
  ],
  category: [
    { value: 'all-new-arrivals', label: 'All New Arrivals', checked: false },
    { value: 'tees', label: 'Tees', checked: false },
    { value: 'objects', label: 'Objects', checked: false },
    { value: 'sweatshirts', label: 'Sweatshirts', checked: false },
    { value: 'pants-and-shorts', label: 'Pants & Shorts', checked: false },
  ],
}
const sortOptions = [
  { name: 'Most Popular', href: '#', current: true },
  { name: 'Best Rating', href: '#', current: false },
  { name: 'Newest', href: '#', current: false },
  { name: 'Price: Low to High', href: '#', current: false },
  { name: 'Price: High to Low', href: '#', current: false },
]
const products = [
  {
    id: 1,
    name: 'Organize Basic Set (Walnut)',
    price: '$149',
    rating: 5,
    reviewCount: 38,
    imageSrc: 'https://tailwindui.com/img/ecommerce-images/category-page-05-image-card-01.jpg',
    imageAlt: 'TODO',
    href: '#',
  },
  {
    id: 2,
    name: 'Organize Pen Holder',
    price: '$15',
    rating: 5,
    reviewCount: 18,
    imageSrc: 'https://tailwindui.com/img/ecommerce-images/category-page-05-image-card-02.jpg',
    imageAlt: 'TODO',
    href: '#',
  },
  {
    id: 3,
    name: 'Organize Sticky Note Holder',
    price: '$15',
    rating: 5,
    reviewCount: 14,
    imageSrc: 'https://tailwindui.com/img/ecommerce-images/category-page-05-image-card-03.jpg',
    imageAlt: 'TODO',
    href: '#',
  },
  {
    id: 4,
    name: 'Organize Phone Holder',
    price: '$15',
    rating: 4,
    reviewCount: 21,
    imageSrc: 'https://tailwindui.com/img/ecommerce-images/category-page-05-image-card-04.jpg',
    imageAlt: 'TODO',
    href: '#',
  },
  // More products...
]
</script>

<template>
  <main class="pb-24">
    <div class="px-4 py-16 text-center sm:px-6 lg:px-8">
      <h1 class="text-4xl font-bold tracking-tight text-gray-900">VS Movies</h1>
      <p class="mx-auto mt-4 max-w-xl text-base text-gray-500">The secret to a tidy desk? Don't get rid of anything, just put it in really really nice looking containers.</p>
    </div>

    <!-- Filters -->
    <Disclosure as="section" aria-labelledby="filter-heading" class="grid items-center border-b border-t border-gray-200">
      <h2 id="filter-heading" class="sr-only">Filters</h2>
      <div class="relative col-start-1 row-start-1 py-4">
        <div class="mx-auto flex max-w-7xl space-x-6 divide-x divide-gray-200 px-4 text-sm sm:px-6 lg:px-8">
          <div>
            <DisclosureButton class="group flex items-center font-medium text-gray-700">
              <FunnelIcon class="mr-2 h-5 w-5 flex-none text-gray-400 group-hover:text-gray-500" aria-hidden="true" />
              2 Filters
            </DisclosureButton>
          </div>
          <div class="pl-6">
            <button type="button" class="text-gray-500">Clear all</button>
          </div>
        </div>
      </div>
      <DisclosurePanel class="border-t border-gray-200 py-10">
        <div class="mx-auto grid max-w-7xl grid-cols-2 gap-x-4 px-4 text-sm sm:px-6 md:gap-x-6 lg:px-8">
          <div class="grid auto-rows-min grid-cols-1 gap-y-10 md:grid-cols-2 md:gap-x-6">
            <fieldset>
              <legend class="block font-medium">Price</legend>
              <div class="space-y-6 pt-6 sm:space-y-4 sm:pt-4">
                <div v-for="(option, optionIdx) in filters.price" :key="option.value" class="flex items-center text-base sm:text-sm">
                  <input :id="`price-${optionIdx}`" name="price[]" :value="option.value" type="checkbox" class="h-4 w-4 flex-shrink-0 rounded border-gray-300 text-indigo-600 focus:ring-indigo-500" :checked="option.checked" />
                  <label :for="`price-${optionIdx}`" class="ml-3 min-w-0 flex-1 text-gray-600">{{ option.label }}</label>
                </div>
              </div>
            </fieldset>
            <fieldset>
              <legend class="block font-medium">Color</legend>
              <div class="space-y-6 pt-6 sm:space-y-4 sm:pt-4">
                <div v-for="(option, optionIdx) in filters.color" :key="option.value" class="flex items-center text-base sm:text-sm">
                  <input :id="`color-${optionIdx}`" name="color[]" :value="option.value" type="checkbox" class="h-4 w-4 flex-shrink-0 rounded border-gray-300 text-indigo-600 focus:ring-indigo-500" :checked="option.checked" />
                  <label :for="`color-${optionIdx}`" class="ml-3 min-w-0 flex-1 text-gray-600">{{ option.label }}</label>
                </div>
              </div>
            </fieldset>
          </div>
          <div class="grid auto-rows-min grid-cols-1 gap-y-10 md:grid-cols-2 md:gap-x-6">
            <fieldset>
              <legend class="block font-medium">Size</legend>
              <div class="space-y-6 pt-6 sm:space-y-4 sm:pt-4">
                <div v-for="(option, optionIdx) in filters.size" :key="option.value" class="flex items-center text-base sm:text-sm">
                  <input :id="`size-${optionIdx}`" name="size[]" :value="option.value" type="checkbox" class="h-4 w-4 flex-shrink-0 rounded border-gray-300 text-indigo-600 focus:ring-indigo-500" :checked="option.checked" />
                  <label :for="`size-${optionIdx}`" class="ml-3 min-w-0 flex-1 text-gray-600">{{ option.label }}</label>
                </div>
              </div>
            </fieldset>
            <fieldset>
              <legend class="block font-medium">Category</legend>
              <div class="space-y-6 pt-6 sm:space-y-4 sm:pt-4">
                <div v-for="(option, optionIdx) in filters.category" :key="option.value" class="flex items-center text-base sm:text-sm">
                  <input :id="`category-${optionIdx}`" name="category[]" :value="option.value" type="checkbox" class="h-4 w-4 flex-shrink-0 rounded border-gray-300 text-indigo-600 focus:ring-indigo-500" :checked="option.checked" />
                  <label :for="`category-${optionIdx}`" class="ml-3 min-w-0 flex-1 text-gray-600">{{ option.label }}</label>
                </div>
              </div>
            </fieldset>
          </div>
        </div>
      </DisclosurePanel>
      <div class="col-start-1 row-start-1 py-4">
        <div class="mx-auto flex max-w-7xl justify-end px-4 sm:px-6 lg:px-8">
          <Menu as="div" class="relative inline-block">
            <div class="flex">
              <MenuButton class="group inline-flex justify-center text-sm font-medium text-gray-700 hover:text-gray-900">
                Sort
                <ChevronDownIcon class="-mr-1 ml-1 h-5 w-5 flex-shrink-0 text-gray-400 group-hover:text-gray-500" aria-hidden="true" />
              </MenuButton>
            </div>

            <transition enter-active-class="transition ease-out duration-100" enter-from-class="transform opacity-0 scale-95" enter-to-class="transform opacity-100 scale-100" leave-active-class="transition ease-in duration-75" leave-from-class="transform opacity-100 scale-100" leave-to-class="transform opacity-0 scale-95">
              <MenuItems class="absolute right-0 z-10 mt-2 w-40 origin-top-right rounded-md bg-white shadow-2xl ring-1 ring-black ring-opacity-5 focus:outline-none">
                <div class="py-1">
                  <MenuItem v-for="option in sortOptions" :key="option.name" v-slot="{ active }">
                    <a :href="option.href" :class="[option.current ? 'font-medium text-gray-900' : 'text-gray-500', active ? 'bg-gray-100' : '', 'block px-4 py-2 text-sm']">{{ option.name }}</a>
                  </MenuItem>
                </div>
              </MenuItems>
            </transition>
          </Menu>
        </div>
      </div>
    </Disclosure>

    <!-- Product grid -->
    <section aria-labelledby="products-heading" class="mx-auto max-w-7xl overflow-hidden sm:px-6 lg:px-8">
      <h2 id="products-heading" class="sr-only">Products</h2>

      <div class="-mx-px grid grid-cols-2 border-l border-gray-200 sm:mx-0 md:grid-cols-3 lg:grid-cols-4">
        <div v-for="product in products" :key="product.id" class="group relative border-b border-r border-gray-200 p-4 sm:p-6">
          <div class="aspect-h-1 aspect-w-1 overflow-hidden rounded-lg bg-gray-200 group-hover:opacity-75">
            <img :src="product.imageSrc" :alt="product.imageAlt" class="h-full w-full object-cover object-center" />
          </div>
          <div class="pb-4 pt-10 text-center">
            <h3 class="text-sm font-medium text-gray-900">
              <a :href="product.href">
                <span aria-hidden="true" class="absolute inset-0" />
                {{ product.name }}
              </a>
            </h3>
            <div class="mt-3 flex flex-col items-center">
              <p class="sr-only">{{ product.rating }} out of 5 stars</p>
              <div class="flex items-center">
                <StarIcon v-for="rating in [0, 1, 2, 3, 4]" :key="rating" :class="[product.rating > rating ? 'text-yellow-400' : 'text-gray-200', 'h-5 w-5 flex-shrink-0']" aria-hidden="true" />
              </div>
              <p class="mt-1 text-sm text-gray-500">{{ product.reviewCount }} reviews</p>
            </div>
            <p class="mt-4 text-base font-medium text-gray-900">{{ product.price }}</p>
          </div>
        </div>
      </div>
    </section>

    <!-- Pagination -->
    <nav aria-label="Pagination" class="mx-auto mt-6 flex max-w-7xl justify-between px-4 text-sm font-medium text-gray-700 sm:px-6 lg:px-8">
      <div class="min-w-0 flex-1">
        <a href="#" class="inline-flex h-10 items-center rounded-md border border-gray-300 bg-white px-4 hover:bg-gray-100 focus:border-indigo-600 focus:outline-none focus:ring-2 focus:ring-indigo-600 focus:ring-opacity-25 focus:ring-offset-1 focus:ring-offset-indigo-600">Previous</a>
      </div>
      <div class="hidden space-x-2 sm:flex">
        <!-- Current: "border-indigo-600 ring-1 ring-indigo-600", Default: "border-gray-300" -->
        <a href="#" class="inline-flex h-10 items-center rounded-md border border-gray-300 bg-white px-4 hover:bg-gray-100 focus:border-indigo-600 focus:outline-none focus:ring-2 focus:ring-indigo-600 focus:ring-opacity-25 focus:ring-offset-1 focus:ring-offset-indigo-600">1</a>
        <a href="#" class="inline-flex h-10 items-center rounded-md border border-gray-300 bg-white px-4 hover:bg-gray-100 focus:border-indigo-600 focus:outline-none focus:ring-2 focus:ring-indigo-600 focus:ring-opacity-25 focus:ring-offset-1 focus:ring-offset-indigo-600">2</a>
        <a href="#" class="inline-flex h-10 items-center rounded-md border border-indigo-600 bg-white px-4 ring-1 ring-indigo-600 hover:bg-gray-100 focus:border-indigo-600 focus:outline-none focus:ring-2 focus:ring-indigo-600 focus:ring-opacity-25 focus:ring-offset-1 focus:ring-offset-indigo-600">3</a>
        <span class="inline-flex h-10 items-center px-1.5 text-gray-500">...</span>
        <a href="#" class="inline-flex h-10 items-center rounded-md border border-gray-300 bg-white px-4 hover:bg-gray-100 focus:border-indigo-600 focus:outline-none focus:ring-2 focus:ring-indigo-600 focus:ring-opacity-25 focus:ring-offset-1 focus:ring-offset-indigo-600">8</a>
        <a href="#" class="inline-flex h-10 items-center rounded-md border border-gray-300 bg-white px-4 hover:bg-gray-100 focus:border-indigo-600 focus:outline-none focus:ring-2 focus:ring-indigo-600 focus:ring-opacity-25 focus:ring-offset-1 focus:ring-offset-indigo-600">9</a>
        <a href="#" class="inline-flex h-10 items-center rounded-md border border-gray-300 bg-white px-4 hover:bg-gray-100 focus:border-indigo-600 focus:outline-none focus:ring-2 focus:ring-indigo-600 focus:ring-opacity-25 focus:ring-offset-1 focus:ring-offset-indigo-600">10</a>
      </div>
      <div class="flex min-w-0 flex-1 justify-end">
        <a href="#" class="inline-flex h-10 items-center rounded-md border border-gray-300 bg-white px-4 hover:bg-gray-100 focus:border-indigo-600 focus:outline-none focus:ring-2 focus:ring-indigo-600 focus:ring-opacity-25 focus:ring-offset-1 focus:ring-offset-indigo-600">Next</a>
      </div>
    </nav>
  </main>
</template>
