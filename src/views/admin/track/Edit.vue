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
        <div class="fixed inset-0 bg-gray-900 bg-opacity-75 transition-opacity" />
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
              class="relative transform overflow-hidden rounded-lg bg-gray-800 px-4 pb-4 pt-5 text-white shadow-xl transition-all sm:my-8 sm:w-full sm:max-w-lg sm:p-6"
            >
              <form v-on:submit.prevent="saveTrack">
                <div>
                  <div class="mt-3 sm:mt-5">
                    <DialogTitle as="h3" class="text-base font-semibold leading-6">
                      {{ track.name }}
                    </DialogTitle>
                    <div class="mt-2">
                      <div class="grid max-w-2xl grid-cols-1 gap-x-6 gap-y-4 sm:grid-cols-6">
                        <!-- Name -->
                        <div class="sm:col-span-8">
                          <label for="name" class="block text-sm font-medium leading-6 text-gray-400">Name</label>
                          <div class="mt-1 relative rounded-md shadow-sm">
                            <input
                              type="text"
                              name="name"
                              id="name"
                              class="block w-full border-gray-300 rounded-md bg-gray-700 text-white focus:ring-indigo-500 focus:border-indigo-500 transition duration-150 ease-in-out sm:text-sm sm:leading-5"
                              v-model="track.name"
                            />
                          </div>
                        </div>
                        <!-- File -->
                        <div class="sm:col-span-8">
                          <label for="file" class="block text-sm font-medium leading-6 text-gray-400">File</label>
                          <div class="mt-1 relative rounded-md shadow-sm">
                            <input
                              type="file"
                              name="file"
                              id="file"
                              class="block w-full border-gray-300 rounded-md bg-gray-700 text-white focus:ring-indigo-500 focus:border-indigo-500 transition duration-150 ease-in-out sm:text-sm sm:leading-5"
                              @change="handleFileUpload"
                            />
                          </div>
                        </div>
                        <!-- Genre -->
                        <div class="sm:col-span-4">
                          <label for="genre" class="block text-sm font-medium leading-6 text-gray-400">Genre</label>
                          <div class="mt-1 relative rounded-md shadow-sm">
                            <input
                              type="text"
                              name="genre"
                              id="genre"
                              class="block w-full border-gray-300 rounded-md bg-gray-700 text-white focus:ring-indigo-500 focus:border-indigo-500 transition duration-150 ease-in-out sm:text-sm sm:leading-5"
                              v-model="track.genre"
                            />
                          </div>
                        </div>
                        <!-- Duration -->
                        <div class="sm:col-span-4">
                          <label for="duration" class="block text-sm font-medium leading-6 text-gray-400">Duration</label>
                          <div class="mt-1 relative rounded-md shadow-sm">
                            <input
                              type="number"
                              name="duration"
                              id="duration"
                              class="block w-full border-gray-300 rounded-md bg-gray-700 text-white focus:ring-indigo-500 focus:border-indigo-500 transition duration-150 ease-in-out sm:text-sm sm:leading-5"
                              v-model="track.duration"
                            />
                          </div>
                        </div>
                        <!-- Artist -->
                        <div class="sm:col-span-8">
                          <label for="artist" class="block text-sm font-medium leading-6 text-gray-400">Artist</label>
                          <div class="mt-1 relative rounded-md shadow-sm">
                            <input
                              type="text"
                              name="artist"
                              id="artist"
                              class="block w-full border-gray-300 rounded-md bg-gray-700 text-white focus:ring-indigo-500 focus:border-indigo-500 transition duration-150 ease-in-out sm:text-sm sm:leading-5"
                              v-model="track.artist"
                            />
                          </div>
                        </div>
                        <!-- Album -->
                        <div class="sm:col-span-8">
                          <label for="album" class="block text-sm font-medium leading-6 text-gray-400">Album</label>
                          <div class="mt-1 relative rounded-md shadow-sm">
                            <input
                              type="text"
                              name="album"
                              id="album"
                              class="block w-full border-gray-300 rounded-md bg-gray-700 text-white focus:ring-indigo-500 focus:border-indigo-500 transition duration-150 ease-in-out sm:text-sm sm:leading-5"
                              v-model="track.album"
                            />
                          </div>
                        </div>
                        <!-- Status -->
                        <div class="sm:col-span-4">
                          <label for="status" class="block text-sm font-medium leading-6 text-gray-400">Status</label>
                          <div class="mt-1 relative rounded-md shadow-sm">
                            <select
                              v-model="track.status"
                              name="status"
                              id="status"
                              class="block w-full border-gray-300 rounded-md bg-gray-700 text-white focus:ring-indigo-500 focus:border-indigo-500 transition duration-150 ease-in-out sm:text-sm sm:leading-5"
                            >
                              <option value="true">Active</option>
                              <option value="false">Inactive</option>
                            </select>
                          </div>
                        </div>

                        <!-- Dynamic Information Display -->
                        <div class="sm:col-span-8">
                          <div class="text-sm text-gray-500">
                            <ul>
                              <li>Name: {{ track.name }}</li>
                              <li>Genre: {{ track.genre }}</li>
                              <li>Duration: {{ track.duration }} sec</li>
                              <li>Artist: {{ track.artist }}</li>
                              <li>Album: {{ track.album }}</li>
                              <li>Status: {{ track.status ? 'Active' : 'Inactive' }}</li>
                            </ul>
                          </div>
                        </div>
                      </div>
                    </div>
                  </div>
                </div>
                <div class="mt-5 sm:mt-6 flex gap-8">
                  <RouterLink
                    type="button"
                    class="mt-3 inline-flex w-full justify-center rounded-md bg-white px-3 py-2 text-sm font-semibold text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 hover:bg-gray-50 sm:col-start-1 sm:mt-0"
                    to="/admin/track"
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

const saveTrack = () => {
  console.log(track.value)

  // route the user to the track list page
  router.push('/admin/track')
}

const handleFileUpload = (event) => {
  const file = event.target.files[0]
  // Here you can handle the file upload process, like sending it to a server or displaying it preview
  console.log('Uploaded file:', file)
}
</script>

<style></style>
