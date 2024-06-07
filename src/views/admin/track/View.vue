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
        <div class="flex min-h-full items-end justify-center p-4 text-center sm:items-center sm:p-0">
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
                    {{ track.name }}
                  </DialogTitle>
                  <div class="mt-2">
                    <div class="text-sm">
                      <ul>
                        <li><strong>File:</strong> <a :href="track.file" class="text-indigo-600 hover:text-indigo-400">Download</a></li>
                        <li><strong>Genre:</strong> {{ track.genre }}</li>
                        <li><strong>Duration:</strong> {{ track.duration }} sec</li>
                        <li><strong>Artist:</strong> {{ track.artist }}</li>
                        <li><strong>Album:</strong> {{ track.album }}</li>
                        <li><strong>Status:</strong> {{ track.status ? 'Active' : 'Inactive' }}</li>
                      </ul>
                    </div>
                  </div>
                </div>
              </div>
              <div class="mt-5 sm:mt-6">
                <RouterLink
                  type="button"
                  class="mt-3 inline-flex w-full justify-center rounded-md bg-red-600 px-3 py-2 text-sm font-semibold text-white shadow-sm ring-1 ring-inset ring-red-700 hover:bg-red-500 sm:col-start-1 sm:mt-0"
                  to="/admin/track"
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
import { RouterLink } from 'vue-router'

const open = ref(true)

const track = ref({
  id: 1,
  name: "Track 1",
  file: "path/to/track1.mp3",
  genre: "RAP",
  duration: 185,
  artist: "Artist 1",
  album: "Album 1",
  status: true,
})

const tracks = ref([
  {
    id: 1,
    name: "Track 1",
    file: "path/to/track1.mp3",
    genre: "RAP",
    duration: 185,
    artist: "Artist 1",
    album: "Album 1",
    sort_order: 0,
    status: true
  },
  {
    id: 2,
    name: "Track 2",
    file: "path/to/track2.mp3",
    genre: "POP",
    duration: 200,
    artist: "Artist 2",
    album: "Album 2",
    sort_order: 1,
    status: true
  },
  {
    id: 3,
    name: "Track 3",
    file: "path/to/track3.mp3",
    genre: "ROCK",
    duration: 240,
    artist: "Artist 3",
    album: "Album 3",
    sort_order: 2,
    status: false
  },
  // Add more tracks as needed
])
</script>

<style></style>
