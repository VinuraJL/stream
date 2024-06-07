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
          
        </div>

        

        <div class="mt-4 sm:ml-16 sm:mt-0 sm:flex-none">
          <RouterLink
            to="/admin/artist/create"
            type="button"
            class="block rounded-md bg-indigo-600 px-3 py-2 text-center text-sm font-semibold text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600">
            Add Artist
          </RouterLink>
        </div>
      </div>
      <div class="mt-8 flow-root">
        <div class="-mx-4 -my-2 overflow-x-auto sm:-mx-6 lg:-mx-8">
          <div class="inline-block min-w-full py-2 align-middle sm:px-6 lg:px-8">
            <table class="min-w-full divide-y divide-gray-300">
              <thead>
                <tr>
                  <th
                    scope="col"
                    class="py-3.5 pl-4 pr-3 text-left text-sm font-semibold text-gray-900 sm:pl-0"
                  >
                    ID
                  </th>
                  <th scope="col" class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900">
                    Avatar
                  </th>
                  <th scope="col" class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900">
                    Name
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
  <tr v-for="artist in artists" :key="artist.id">
    <td
      class="whitespace-nowrap py-4 pl-4 pr-3 text-sm font-medium text-gray-900 sm:pl-0"
    >
      {{ artist.id }}
    </td>
    <td class="py-4 pl-3 pr-4 text-sm text-gray-500">
      <img :src="artist.avatar" alt="Artist Avatar" class="h-8 w-8 rounded-full mr-2">
    </td>
    <td class="whitespace-nowrap py-4 text-sm text-gray-500">
      {{ artist.name }}
    </td>
    <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">
      <span v-if="artist.status">Active</span>
      <span v-else>Inactive</span>
    </td>
    <td
      class="relative whitespace-nowrap py-4 pl-3 pr-4 text-right text-sm font-medium sm:pr-0"
    >
      <RouterLink
        :to="`/admin/artist/${artist.id}`"
        class="text-indigo-600 hover:text-indigo-900"
      >
        View
        <span class="sr-only">, {{ artist.name }}</span>
      </RouterLink>
      |
      <RouterLink
        :to="`/admin/artist/${artist.id}/edit`"
        class="text-indigo-600 hover:text-indigo-900"
      >
        Edit
        <span class="sr-only">, {{ artist.name }}</span>
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
import { Menu, MenuButton, MenuItems, MenuItem } from '@headlessui/vue'
import { Bars3Icon, XMarkIcon, BellIcon } from '@heroicons/vue/24/outline'
import { RouterLink } from 'vue-router'

const navigation = [


 
  { name: 'Albums', href: '/admin/album', current: false },
  { name: 'Artists', href: '/admin/artist', current: true },
  { name: 'Genres', href: '/admin/genre', current: false },
  { name: 'Tracks', href: '/admin/track', current: false },
  { name: 'Users', href: '/admin/users', current: false },
  { name: 'Sign Out', href: '/', current: false },
]

const artists = ref([]);

fetch('https://t0nwhviu23.execute-api.ap-southeast-1.amazonaws.com/dev/artists')
  .then((response) => response.json())
  .then((response) => {
    console.log(response)
    artists.value = response.body
  })

// const artists = [
//   {
//     id: 1,
//     name: "The Weekend",
//     avatar: "https://www.theweeknd.com/files/2021/10/photo_202110_07_GENERAL-BRIANZIFF_THEWEEKND_1323-crop-1.jpeg",
//     sort_order: 0,
//     status: true
//   },

//   {
//     id: 2,
//     name: "Eminem",
//     avatar: "https://variety.com/wp-content/uploads/2024/02/Eminem.jpg",
//     sort_order: 0,
//     status: true
//   },

//   {
//     id: 3,
//     name: "Chase Atlantic",
//     avatar: "https://i.scdn.co/image/ab67616d0000b273601eb33454f13f26db9084e4",
//     sort_order: 0,
//     status: true
//   },

//   {
//     id: 4,
//     name: "Metro Boomin",
//     avatar: "https://i.scdn.co/image/ab6761610000e5ebdf9a1555f53a20087b8c5a5c",
//     sort_order: 0,
//     status: true
//   },
  
//   {
//     id: 5,
//     name: "Twenty One Pilots",
//     avatar: "https://i.scdn.co/image/ab67616100005174274df4dfcb960867eccedfb5",
//     sort_order: 0,
//     status: true
//   },

//   {
//     id: 6,
//     name: "NF",
//     avatar: "https://i.scdn.co/image/ab6761610000e5eb1cf142a710a2f3d9b7a62da1",
//     sort_order: 0,
//     status: true
//   },
//   {
//     id: 7,
//     name: "Billie Eilish",
//     avatar: "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRa8y2lpu2cIA3u5bQmHTlXvg2occRyApI_7A&s",
//     sort_order: 1,
//     status: true
//   },
//   {
//     id: 8,
//     name: "YUNGBLUD",
//     avatar: "https://i.scdn.co/image/ab6761610000e5ebc733e03049f72ac47bee8259",
//     sort_order: 2,
//     status: true
//   },
//   {
//     id: 9,
//     name: "Dua Lipa",
//     avatar: "https://i.scdn.co/image/ab67616d00001e02b627441824c5d0748c8cb077",
//     sort_order: 3,
//     status: true
//   },
//   {
//     id: 10,
//     name: "Post Malone",
//     avatar: "https://i.scdn.co/image/ab67616d00001e0255404f712deb84d0650a4b41",
//     sort_order: 4,
//     status: true
//   },
//   {
//     id: 11,
//     name: "Ariana Grande",
//     avatar: "https://i.scdn.co/image/ab6761610000e5eb40b5c07ab77b6b1a9075fdc0",
//     sort_order: 5,
//     status: true
//   },
//   {
//     id: 12,
//     name: "Drake",
//     avatar: "https://i.scdn.co/image/ab6761610000e5eb4293385d324db8558179afd9",
//     sort_order: 6,
//     status: true
//   },
//   {
//     id: 13,
//     name: "Taylor Swift",
//     avatar: "https://i.scdn.co/image/ab6761610000e5ebe672b5f553298dcdccb0e676",
//     sort_order: 7,
//     status: true
//   },
//   {
//     id: 14,
//     name: "Bruno Mars",
//     avatar: "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRxkzAkVne1rmBK0WxWy_G8Ht-fUTTHZ7oUmg&s",
//     sort_order: 8,
//     status: true
//   },

//   // Add more artists as needed
// ]
</script>

<style></style>
