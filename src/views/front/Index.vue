<template>
  <div>
    <!-- Navbar -->
    <Disclosure as="nav" class="bg-gray-800" v-slot="{ open }">
      <div class="mx-auto max-w-7xl px-2 sm:px-6 lg:px-8">
        <div class="relative flex h-16 items-center justify-between">
          <div class="absolute inset-y-0 left-0 flex items-center sm:hidden">
            <!-- Mobile menu button-->
            <DisclosureButton class="relative inline-flex items-center justify-center rounded-md p-2 text-gray-400 hover:bg-gray-700 hover:text-white focus:outline-none focus:ring-2 focus:ring-inset focus:ring-white">
              <span class="absolute -inset-0.5" />
              <span class="sr-only">Open main menu</span>
              <Bars3Icon v-if="!open" class="block h-6 w-6" aria-hidden="true" />
              <XMarkIcon v-else class="block h-6 w-6" aria-hidden="true" />
            </DisclosureButton>
          </div>
          <div class="flex flex-1 items-center justify-center sm:items-stretch sm:justify-start">
            <div class="flex flex-shrink-0 items-center">
              <img class="h-8 w-auto" src="https://tailwindui.com/img/logos/mark.svg?color=indigo&shade=500" alt="Your Company" />
            </div>
            <div class="hidden sm:ml-6 sm:block">
              <div class="flex space-x-4">
                <RouterLink
                  v-for="item in navigation"
                  :key="item.name"
                  :to="item.href"
                  :class="[item.current ? 'bg-gray-900 text-white' : 'text-gray-300 hover:bg-gray-700 hover:text-white', 'rounded-md px-3 py-2 text-sm font-medium']"
                  :aria-current="item.current ? 'page' : undefined"
                >
                  {{ item.name }}
                </RouterLink>
              </div>
            </div>
          </div>
        </div>
      </div>

      <DisclosurePanel class="sm:hidden">
        <div class="space-y-1 px-2 pb-3 pt-2">
          <DisclosureButton
            v-for="item in navigation"
            :key="item.name"
            as="a"
            :to="item.href"
            :class="[item.current ? 'bg-gray-900 text-white' : 'text-gray-300 hover:bg-gray-700 hover:text-white', 'block rounded-md px-3 py-2 text-base font-medium']"
            :aria-current="item.current ? 'page' : undefined"
          >
            {{ item.name }}
          </DisclosureButton>
        </div>
      </DisclosurePanel>
    </Disclosure>

    <!-- Main content -->
    <div class="px-4 sm:px-6 lg:px-8">
      <div class="sm:flex sm:items-center">
        <div class="sm:flex-auto">
          <h1 class="text-xl font-semibold text-gray-900">Albums</h1>
        </div>
      </div>

      <!-- Album Tiles -->
      <div class="mt-8 grid grid-cols-1 gap-6 sm:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4">
        <div 
          v-for="album in albums" 
          :key="album.id" 
          class="relative flex flex-col items-center rounded-lg border border-gray-200 bg-white p-6 shadow-md hover:bg-gray-100 transition duration-300 ease-in-out"
          @click="showAlbumDetails"
        >
          <img :src="album.album_art" alt="Album Art" class="h-32 w-32 rounded-md object-cover">
          <h3 class="mt-4 text-lg font-medium text-gray-900">{{ album.name }}</h3>
          <p class="mt-1 text-sm text-gray-500">{{ album.artist.name }}</p>
          <p class="mt-1 text-sm text-gray-500">{{ album.year }}</p>
          <p class="mt-1 text-sm text-gray-500">{{ album.genre }}</p>
          <div class="absolute inset-0 flex items-center justify-center bg-black bg-opacity-50 text-white opacity-0 hover:opacity-100 transition duration-300 ease-in-out">
            <div class="text-center">
              <p>ID: {{ album.id }}</p>
              <p>Studio: {{ album.studio }}</p>
              <p>Status: <span v-if="album.status">Active</span><span v-else>Inactive</span></p>
            </div>
          </div>
        </div>
      </div>
    </div>
    
    <!-- Album Details Modal -->
    <div v-if="showModal" class="fixed inset-0 flex items-center justify-center bg-black bg-opacity-50">
      <div class="bg-white rounded-lg p-6">
        <h2 class="text-2xl font-bold mb-4">{{ selectedAlbum.name }}</h2>
        <img :src="selectedAlbum.album_art" alt="Album Art" class="w-full h-64 object-cover rounded-lg mb-4">
        <p class="text-sm text-gray-500">Artist: {{ selectedAlbum.artist.name }}</p>
        <p class="text-sm text-gray-500">Year: {{ selectedAlbum.year }}</p>
        <p class="text-sm text-gray-500">Number of Tracks: {{ selectedAlbum.number_of_tracks }}</p>
        <button @click="closeModal" class="mt-4 px-4 py-2 bg-indigo-600 text-white rounded-md hover:bg-indigo-500">Close</button>
      </div>
    </div>

    <router-view />
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { Disclosure, DisclosureButton, DisclosurePanel } from '@headlessui/vue'
import { Bars3Icon, XMarkIcon } from '@heroicons/vue/24/outline'
import { RouterLink } from 'vue-router'

const navigation = [
 
  { name: 'Albums', href: '/front/album', current: true },
  { name: 'Artists', href: '/front/artist', current: false },
  { name: 'Genres', href: '/front/genre', current: false },
  { name: 'Tracks', href: '/front/track', current: false },
  
]

const albums = ref([])

fetch('https://t0nwhviu23.execute-api.ap-southeast-1.amazonaws.com/dev/albums')
  .then((response) => response.json())
  .then((response) => {
    console.log(response)
    albums.value = response.body
  })

const showModal = ref(false)
const selectedAlbum = ref({
  id: 1,
  name: 'The After Hours',
  number_of_tracks: 8,
  year: 2020,
  album_art: 'https://image-cdn.hypb.st/https%3A%2F%2Fhypebeast.com%2Fimage%2F2020%2F03%2Fthe-weeknd-after-hours-album-stream-listen-1.jpg?cbr=1&q=90',
  artist: {
    id: 8,
    name: 'The Weeknd',
    avatar: 'IMAGE_URL'
  }
})

const showAlbumDetails = () => {
  showModal.value = true
}

const closeModal = () => {
  showModal.value = false
}
</script>

<style scoped>
/* Add any additional styling you need here */
</style>
