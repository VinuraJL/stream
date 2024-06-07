<template>
  <TransitionRoot as="template" :show="open">
    <Dialog as="div" class="relative z-10" @close="open = false">
      <TransitionChild
        as="template"
        enter="ease-out duration-300"
        enter-from="opacity-0"
        enter-to="opacity-100"
        leave="ease-in duration-200"
        leave-from="opacity-100"
        leave-to="opacity-0"
      >
        <div class="fixed inset-0 bg-gray-500 bg-opacity-75 transition-opacity" />
      </TransitionChild>

      <div class="fixed inset-0 z-10 w-screen overflow-y-auto">
        <div
          class="flex min-h-full items-end justify-center p-4 text-center sm:items-center sm:p-0"
        >
          <TransitionChild
            as="template"
            enter="ease-out duration-300"
            enter-from="opacity-0 translate-y-4 sm:translate-y-0 sm:scale-95"
            enter-to="opacity-100 translate-y-0 sm:scale-100"
            leave="ease-in duration-200"
            leave-from="opacity-100 translate-y-0 sm:scale-100"
            leave-to="opacity-0 translate-y-4 sm:translate-y-0 sm:scale-95"
          >
            <DialogPanel
              class="relative transform overflow-hidden rounded-lg bg-gray-800 px-4 pb-4 pt-5 text-white shadow-xl transition-all sm:my-8 sm:w-full sm:max-w-lg sm:p-6 text-left"
            >
              <div>
                <div class="mt-3 sm:mt-5">
                  <DialogTitle as="h3" class="text-lg font-semibold leading-6">
                    {{ album.name }}
                  </DialogTitle>
                  <div class="mt-2">
                    <div class="text-sm">
                      <ul>
                        <li><strong>Number of Tracks:</strong> {{ album.number_of_tracks }}</li>
                        <li><strong>Year:</strong> {{ album.year }}</li>
                        <li><strong>Album Art:</strong> {{ album.album_art }}</li>
                        <li><strong>Artist:</strong> {{ album.artist.name }}</li>
                        <li><strong>Studio:</strong> {{ album.studio }}</li>
                        <li><strong>Genre:</strong> {{ album.genre }}</li>
                        <li><strong>Sort Order:</strong> {{ album.sort_order }}</li>
                        <li><strong>Status:</strong> {{ album.status ? 'Active' : 'Inactive' }}</li>
                      </ul>
                    </div>
                  </div>
                </div>
              </div>
              <div class="mt-5 sm:mt-6">
                <RouterLink
                  type="button"
                  class="mt-3 inline-flex w-full justify-center rounded-md bg-red-600 px-3 py-2 text-sm font-semibold text-white shadow-sm ring-1 ring-inset ring-red-700 hover:bg-red-500 sm:col-start-1 sm:mt-0"
                  to="/admin/album"
                  ref="cancelButtonRef"
                >
                  Close
                </RouterLink>
              </div>
            </DialogPanel>
          </TransitionChild>
        </div>
      </div>
    </Dialog>
  </TransitionRoot>
</template>

<script setup>
import { ref } from 'vue'
import { Dialog, DialogPanel, DialogTitle, TransitionChild, TransitionRoot } from '@headlessui/vue'
import { CheckIcon } from '@heroicons/vue/24/outline'

const open = ref(true)

const album = {
  id: 1,
  name: 'Paata',
  number_of_tracks: 8,
  year: 2020,
  album_art: 'IMAGE_URL',
  artist: {
    id: 1,
    name: 'Costa',
    avatar: 'IMAGE_URL'
  },
  studio: 'COSTA Songs',
  genre: 'RAP',
  sort_order: 0,
  status: true // Published etc.
}
</script>
