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
              <form v-on:submit.prevent="saveUser">
                <div>
                  <div class="mt-3 sm:mt-5">
                    <DialogTitle as="h3" class="text-base font-semibold leading-6">
                      {{ user.first_name }} {{ user.last_name }}
                    </DialogTitle>
                    <div class="mt-2">
                      <div class="grid max-w-2xl grid-cols-1 gap-x-6 gap-y-4 sm:grid-cols-6">
                        <!-- First Name -->
                        <div class="sm:col-span-8">
                          <label for="first_name" class="block text-sm font-medium leading-6 text-white">First Name</label>
                          <div class="mt-2">
                            <div class="flex rounded-md shadow-sm ring-1 ring-inset ring-white focus-within:ring-2 focus-within:ring-inset focus-within:ring-indigo-600 sm:max-w-md">
                              <input
                                type="text"
                                name="first_name"
                                id="first_name"
                                class="block flex-1 border-0 bg-transparent py-1.5 pl-1 text-white placeholder:text-gray-400 focus:ring-0 sm:text-sm sm:leading-6"
                                v-model="user.first_name"
                              />
                            </div>
                          </div>
                        </div>

                        <!-- Last Name -->
                        <div class="sm:col-span-8">
                          <label for="last_name" class="block text-sm font-medium leading-6 text-white">Last Name</label>
                          <div class="mt-2">
                            <div class="flex rounded-md shadow-sm ring-1 ring-inset ring-white focus-within:ring-2 focus-within:ring-inset focus-within:ring-indigo-600 sm:max-w-md">
                              <input
                                type="text"
                                name="last_name"
                                id="last_name"
                                class="block flex-1 border-0 bg-transparent py-1.5 pl-1 text-white placeholder:text-gray-400 focus:ring-0 sm:text-sm sm:leading-6"
                                v-model="user.last_name"
                              />
                            </div>
                          </div>
                        </div>

                        <!-- Email -->
                        <div class="sm:col-span-8">
                          <label for="email" class="block text-sm font-medium leading-6 text-white">Email</label>
                          <div class="mt-2">
                            <div class="flex rounded-md shadow-sm ring-1 ring-inset ring-white focus-within:ring-2 focus-within:ring-inset focus-within:ring-indigo-600 sm:max-w-md">
                              <input
                                type="email"
                                name="email"
                                id="email"
                                class="block flex-1 border-0 bg-transparent py-1.5 pl-1 text-white placeholder:text-gray-400 focus:ring-0 sm:text-sm sm:leading-6"
                                v-model="user.email"
                              />
                            </div>
                          </div>
                        </div>

                        <!-- Password -->
                        <div class="sm:col-span-8">
                          <label for="password" class="block text-sm font-medium leading-6 text-white">Password</label>
                          <div class="mt-2">
                            <div class="flex rounded-md shadow-sm ring-1 ring-inset ring-white focus-within:ring-2 focus-within:ring-inset focus-within:ring-indigo-600 sm:max-w-md">
                              <input
                                type="password"
                                name="password"
                                id="password"
                                class="block flex-1 border-0 bg-transparent py-1.5 pl-1 text-white placeholder:text-gray-400 focus:ring-0 sm:text-sm sm:leading-6"
                                v-model="user.password"
                              />
                            </div>
                          </div>
                        </div>

                        <!-- Age -->
                        <div class="sm:col-span-4">
                          <label for="age" class="block text-sm font-medium leading-6 text-white">Age</label>
                          <div class="mt-2">
                            <div class="flex rounded-md shadow-sm ring-1 ring-inset ring-white focus-within:ring-2 focus-within:ring-inset focus-within:ring-indigo-600 sm:max-w-md">
                              <input
                                type="number"
                                name="age"
                                id="age"
                                class="block flex-1 border-0 bg-transparent py-1.5 pl-1 text-white placeholder:text-gray-400 focus:ring-0 sm:text-sm sm:leading-6"
                                v-model="user.age"
                              />
                            </div>
                          </div>
                        </div>

                        <!-- Country -->
                        <div class="sm:col-span-8">
                          <label for="country" class="block text-sm font-medium leading-6 text-white">Country</label>
                          <div class="mt-2">
                            <div class="flex rounded-md shadow-sm ring-1 ring-inset ring-white focus-within:ring-2 focus-within:ring-inset focus-within:ring-indigo-600 sm:max-w-md">
                              <input
                                type="text"
                                name="country"
                                id="country"
                                class="block flex-1 border-0 bg-transparent py-1.5 pl-1 text-white placeholder:text-gray-400 focus:ring-0 sm:text-sm sm:leading-6"
                                v-model="user.country"
                              />
                            </div>
                          </div>
                        </div>

                        <!-- Subscription -->
                        <div class="sm:col-span-8">
                          <label for="subscription" class="block text-sm font-medium leading-6 text-white">Subscription</label>
                          <div class="mt-2">
                            <div class="flex rounded-md shadow-sm ring-1 ring-inset ring-white focus-within:ring-2 focus-within:ring-inset focus-within:ring-indigo-600 sm:max-w-md">
                              <input
                                type="text"
                                name="subscription"
                                id="subscription"
                                class="block flex-1 border-0 bg-transparent py-1.5 pl-1 text-white placeholder:text-gray-400 focus:ring-0 sm:text-sm sm:leading-6"
                                v-model="user.subscription"
                              />
                            </div>
                          </div>
                        </div>

                        <!-- Phone -->
                        <div class="sm:col-span-8">
                          <label for="phone" class="block text-sm font-medium leading-6 text-white">Phone</label>
                          <div class="mt-2">
                            <div class="flex rounded-md shadow-sm ring-1 ring-inset ring-white focus-within:ring-2 focus-within:ring-inset focus-within:ring-indigo-600 sm:max-w-md">
                              <input
                                type="text"
                                name="phone"
                                id="phone"
                                class="block flex-1 border-0 bg-transparent py-1.5 pl-1 text-white placeholder:text-gray-400 focus:ring-0 sm:text-sm sm:leading-6"
                                v-model="user.phone"
                              />
                            </div>
                          </div>
                        </div>

                        <!-- Dynamic Information Display -->
                        <div class="sm:col-span-8">
                          <div class="text-sm text-gray-500">
                            <ul>
                              <li>First Name: {{ user.first_name }}</li>
                              <li>Last Name: {{ user.last_name }}</li>
                              <li>Email: {{ user.email }}</li>
                              <li>Age: {{ user.age }}</li>
                              <li>Country: {{ user.country }}</li>
                              <li>Subscription: {{ user.subscription }}</li>
                              <li>Phone: {{ user.phone }}</li>
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
                    to="/admin/user"
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

const user = ref({
  id: null,
  first_name: 'John',
  last_name: 'Doe',
  email: '',
  password: '',
  age: null,
  country: '',
  subscription: '',
  phone: ''
})

const saveUser = () => {
  console.log(user.value)
  // route the user to the user list page after saving the user data
  router.push('/admin/users')
}

</script>
