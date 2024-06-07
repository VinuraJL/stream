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
        <div class="sm:flex-auto"></div>
        <div class="mt-4 sm:ml-16 sm:mt-0 sm:flex-none">
          <RouterLink
            to="/admin/genre/create"
            type="button"
            class="block rounded-md bg-indigo-600 px-3 py-2 text-center text-sm font-semibold text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600">
            Add Genre
          </RouterLink>
        </div>
      </div>
      <div class="mt-8 flow-root">
        <div class="-mx-4 -my-2 overflow-x-auto sm:-mx-6 lg:-mx-8">
          <div class="inline-block min-w-full py-2 align-middle sm:px-6 lg:px-8">
            <table class="min-w-full divide-y divide-gray-300">
              <thead>
                <tr>
                  <th scope="col" class="py-3.5 pl-4 pr-3 text-left text-sm font-semibold text-gray-900 sm:pl-0">
                    ID
                  </th>
                  <th scope="col" class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900">
                    Image
                  </th>
                  <th scope="col" class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900">
                    Name
                  </th>
                  <th scope="col" class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900">
                    Description
                  </th>
                  <th scope="col" class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900">
                    Status
                  </th>
                  <th scope="col" class="relative py-3.5 pl-3 pr-4 sm:pr-0">
                    <span class="sr-only">Edit</span>
                  </th>
                </tr>
              </thead>
              <tbody class="divide-y divide-gray-200">
                <tr v-for="genre in genres" :key="genre.id">
                  <td class="whitespace-nowrap py-4 pl-4 pr-3 text-sm font-medium text-gray-900 sm:pl-0">
                    {{ genre.id }}
                  </td>
                  <td class="py-4 pl-3 pr-4 text-sm text-gray-500">
                    <img :src="genre.image" alt="Genre Image" class="h-8 w-8 rounded-full mr-2">
                  </td>
                  <td class="whitespace-nowrap py-4 text-sm text-gray-500">
                    {{ genre.name }}
                  </td>
                  <td class="whitespace-nowrap py-4 text-sm text-gray-500">
                    {{ genre.description }}
                  </td>
                  <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">
                    <span v-if="genre.status">Active</span>
                    <span v-else>Inactive</span>
                  </td>
                  <td class="relative whitespace-nowrap py-4 pl-3 pr-4 text-right text-sm font-medium sm:pr-0">
                    <RouterLink :to="`/admin/genre/${genre.id}`" class="text-indigo-600 hover:text-indigo-900">
                      View
                      <span class="sr-only">, {{ genre.name }}</span>
                    </RouterLink>
                    |
                    <RouterLink :to="`/admin/genre/${genre.id}/edit`" class="text-indigo-600 hover:text-indigo-900">
                      Edit
                      <span class="sr-only">, {{ genre.name }}</span>
                    </RouterLink>
                  </td>
                </tr>
              </tbody>
            </table>
          </div>
        </div>
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
 
  { name: 'Admin Dashboard', href: '/AdminDashboard', current: false },
  
  { name: 'Albums', href: '/admin/album', current: false },
  { name: 'Artists', href: '/admin/artist', current: false },
  { name: 'Genres', href: '/admin/genre', current: true },
  { name: 'Tracks', href: '/admin/track', current: false },
  { name: 'Users', href: '/admin/users', current: false }
]

const genres = ref([]);

fetch('https://t0nwhviu23.execute-api.ap-southeast-1.amazonaws.com/dev/genres')
  .then((response) => response.json())
  .then((response) => {
    console.log(response)
    genres.value = response.body
  })

// const genres = ref([
//   {
//     id: 1,
//     name: "RAP",
//     description: "Rap is a musical genre that incorporates rhythmic speech and street vernacular over backing beats.",
//     image: "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSFFK7DRRgPp9CILJfmlK3ZAfkNQG8aFwzgGA&s",
//     sort_order: 0,
//     status: true
//   },
//   {
//     id: 2,
//     name: "POP",
//     description: "Pop music is known for its catchy melodies and wide appeal, often blending elements from various genres.",
//     image: "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTlP1rFJSRI6SM5IY43cWtKgGQhAAVhssggVA&s",
//     sort_order: 1,
//     status: true
//   },
//   {
//     id: 3,
//     name: "ROCK",
//     description: "Rock music is characterized by a strong beat, simple chord progressions, and often revolves around electric guitar.",
//     image: "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQiEiCfvdMPRs28QPgMJiYw7OkEn97JilYUJQ&s",
//     sort_order: 2,
//     status: false
//   },
//   // Add more genres as needed
// ])
</script>

<style></style>
