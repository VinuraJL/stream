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
        <div class="fixed inset-0 bg-gray-800 bg-opacity-75 transition-opacity" />
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
              class="relative transform overflow-hidden rounded-lg bg-gray-800 px-4 pb-4 pt-5 text-white shadow-xl transition-all sm:my-8 sm:w-full sm:max-w-lg sm:p-6"
            >
              <form v-on:submit.prevent="saveAlbum">
                <div>
                  <div class="mt-3 sm:mt-5">
                    <DialogTitle as="h3" class="text-base font-semibold leading-6">
                      {{ album.name }}
                    </DialogTitle>
                    <div class="mt-2">
                      <div class="grid max-w-2xl grid-cols-1 gap-x-6 gap-y-4 sm:grid-cols-6">
  <div class="sm:col-span-8">
    <label for="name" class="block text-sm font-medium leading-6 text-white">Name</label>
    <div class="mt-2">
      <div class="flex rounded-md shadow-sm ring-1 ring-inset ring-white focus-within:ring-2 focus-within:ring-inset focus-within:ring-indigo-600 sm:max-w-md">
        <input type="text" name="name" id="name" class="block flex-1 border-0 bg-transparent py-1.5 pl-1 text-white placeholder:text-gray-400 focus:ring-0 sm:text-sm sm:leading-6" v-model="album.name"/>
      </div>
    </div>
  </div>

  <div class="sm:col-span-4">
    <label for="number_of_tracks" class="block text-sm font-medium leading-6 text-white">Number of Tracks</label>
    <div class="mt-2">
      <div class="flex rounded-md shadow-sm ring-1 ring-inset ring-white focus-within:ring-2 focus-within:ring-inset focus-within:ring-indigo-600 sm:max-w-md">
        <input type="text" name="number_of_tracks" id="number_of_tracks" class="block flex-1 border-0 bg-transparent py-1.5 pl-1 text-white placeholder:text-gray-400 focus:ring-0 sm:text-sm sm:leading-6" v-model="album.number_of_tracks"/>
      </div>
    </div>
  </div>

  <div class="sm:col-span-4">
    <label for="year" class="block text-sm font-medium leading-6 text-white">Year</label>
    <div class="mt-2">
      <div class="flex rounded-md shadow-sm ring-1 ring-inset ring-white focus-within:ring-2 focus-within:ring-inset focus-within:ring-indigo-600 sm:max-w-md">
        <input type="text" name="year" id="year" class="block flex-1 border-0 bg-transparent py-1.5 pl-1 text-white placeholder:text-gray-400 focus:ring-0 sm:text-sm sm:leading-6" v-model="album.year"/>
      </div>
    </div>
  </div>

  <div class="sm:col-span-8">
    <label for="album_art" class="block text-sm font-medium leading-6 text-white">Album Art</label>
    <div class="mt-2">
      <div class="flex rounded-md shadow-sm ring-1 ring-inset ring-white focus-within:ring-2 focus-within:ring-inset focus-within:ring-indigo-600 sm:max-w-md">
        <input type="file" name="album_art" id="album_art" class="block flex-1 border-0 bg-transparent py-1.5 pl-1 text-white placeholder:text-gray-400 focus:ring-0 sm:text-sm sm:leading-6"/>
      </div>
    </div>
  </div>

  <div class="sm:col-span-4">
    <label for="artist" class="block text-sm font-medium leading-6 text-white">Artist</label>
    <div class="mt-2">
      <div class="flex rounded-md shadow-sm ring-1 ring-inset ring-white focus-within:ring-2 focus-within:ring-inset focus-within:ring-indigo-600 sm:max-w-md">
        <select v-model="album.artist.id" name="artist" id="artist" class="block flex-1 border-0 bg-transparent py-1.5 pl-1 text-white placeholder:text-gray-400 focus:ring-0 sm:text-sm sm:leading-6">
          <option value="1">Costa</option>
          <option value="2">K Mac</option>
          <option value="3">Ravi Jay</option>
        </select>
      </div>
    </div>
  </div>

  <div class="sm:col-span-4">
    <label for="studio" class="block text-sm font-medium leading-6 text-white">Studio</label>
    <div class="mt-2">
      <div class="flex rounded-md shadow-sm ring-1 ring-inset ring-white focus-within:ring-2 focus-within:ring-inset focus-within:ring-indigo-600 sm:max-w-md">
        <input type="text" name="studio" id="studio" class="block flex-1 border-0 bg-transparent py-1.5 pl-1 text-white placeholder:text-gray-400 focus:ring-0 sm:text-sm sm:leading-6"/>
      </div>
    </div>
  </div>

  <div class="sm:col-span-4">
    <label for="genre" class="block text-sm font-medium leading-6 text-white">Genre</label>
    <div class="mt-2">
      <div class="flex rounded-md shadow-sm ring-1 ring-inset ring-white focus-within:ring-2 focus-within:ring-inset focus-within:ring-indigo-600 sm:max-w-md">
        <input type="text" name="genre" id="genre" v-model="album.genre" class="block flex-1 border-0 bg-transparent py-1.5 pl-1 text-white placeholder:text-gray-400 focus:ring-0 sm:text-sm sm:leading-6"/>
      </div>
    </div>
  </div>
</div>


                      <div class="text-sm text-gray-500">
                        <ul>
                          <li>number_of_tracks: {{ album.number_of_tracks }}</li>
                          <li>year: {{ album.year }}</li>
                          <li>album_art: {{ album.album_art }}</li>
                          <li>artist: {{ album.artist.name }}</li>
                          <li>studio: {{ album.studio }}</li>
                          <li>genre: {{ album.genre }}</li>
                          <li>sort_order: {{ album.sort_order }}</li>
                          <li>status: {{ album.status }}</li>
                        </ul>
                      </div>
                    </div>
                  </div>
                </div>
                <div class="mt-5 sm:mt-6 flex gap-8">
                  <RouterLink
                    type="button"
                    class="mt-3 inline-flex w-full justify-center rounded-md bg-white px-3 py-2 text-sm font-semibold text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 hover:bg-gray-50 sm:col-start-1 sm:mt-0"
                    to="/admin/album"
                    ref="cancelButtonRef"
                  >
                    Back
                  </RouterLink>
                  <button
                    type="submit"
                    class="inline-flex w-full justify-center rounded-md bg-indigo-600 px-3 py-2 text-sm font-semibold text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600 sm:col-start-2"
                  >
                    Save
                  </button>
                </div>
              </form>
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
import { useRouter } from 'vue-router'

const open = ref(true)

const router = useRouter()

const album = ref({
  id: null,
  name: '',
  number_of_tracks: 0,
  year: new Date().getFullYear(),
  album_art: '',
  artist: {
    id: 1,
    name: 'Costa',
    avatar: 'IMAGE_URL'
  },
  studio: '',
  genre: '',
  sort_order: 0,
  status: false // Published etc.
})

const saveAlbum = () => {
  console.log(album)

  // route the user to the album list page
  router.push('/admin/album')
}
</script>
