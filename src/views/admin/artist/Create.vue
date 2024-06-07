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
              <form v-on:submit.prevent="saveArtist">
                <div>
                  <div class="mt-3 sm:mt-5">
                    <DialogTitle as="h3" class="text-base font-semibold leading-6">
                      {{ artist.name }}
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
                              v-model="artist.name"
                            />
                          </div>
                        </div>
                        <!-- Bio -->
                        <div class="sm:col-span-8">
                          <label for="bio" class="block text-sm font-medium leading-6 text-gray-400">Bio</label>
                          <div class="mt-1 relative rounded-md shadow-sm">
                            <textarea
                              name="bio"
                              id="bio"
                              rows="3"
                              class="block w-full border-gray-300 rounded-md bg-gray-700 text-white focus:ring-indigo-500 focus:border-indigo-500 transition duration-150 ease-in-out sm:text-sm sm:leading-5"
                              v-model="artist.bio"
                            ></textarea>
                          </div>
                        </div>
                        <!-- Avatar -->
                        <div class="sm:col-span-8">
                          <label for="avatar" class="block text-sm font-medium leading-6 text-gray-400">Avatar</label>
                          <div class="mt-1 relative rounded-md shadow-sm">
                            <input
                              type="file"
                              name="avatar"
                              id="avatar"
                              class="block w-full border-gray-300 rounded-md bg-gray-700 text-white focus:ring-indigo-500 focus:border-indigo-500 transition duration-150 ease-in-out sm:text-sm sm:leading-5"
                              @change="handleAvatarUpload"
                            />
                          </div>
                        </div>
                        <!-- Status -->
                        <div class="sm:col-span-4">
                          <label for="status" class="block text-sm font-medium leading-6 text-gray-400">Status</label>
                          <div class="mt-1 relative rounded-md shadow-sm">
                            <select
                              v-model="artist.status"
                              name="status"
                              id="status"
                              class="block w-full border-gray-300 rounded-md bg-gray-700 text-white focus:ring-indigo-500 focus:border-indigo-500 transition duration-150 ease-in-out sm:text-sm sm:leading-5"
                            >
                              <option value="true">Active</option>
                              <option value="false">Inactive</option>
                            </select>
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
                    to="/admin/artist"
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

const artist = ref({
  id: 1,
  name: 'Eminem',
  bio: 'Rapper',
  avatar: 'https://variety.com/wp-content/uploads/2024/02/Eminem.jpg',
  status: true
})

const saveArtist = () => {
  console.log(artist)

  // route the user to the artist list page
  router.push('/admin/artist')
}

const handleAvatarUpload = (event) => {
  const file = event.target.files[0]
  // Here you can handle the file upload process, like sending it to a server or displaying it preview
  console.log('Uploaded file:', file)
}
</script>
