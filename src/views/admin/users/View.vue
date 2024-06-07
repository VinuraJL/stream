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
                    {{ user.first_name }} {{ user.last_name }}
                  </DialogTitle>
                  <div class="mt-2">
                    <div class="text-sm">
                      <ul>
                        <li><strong>Email:</strong> {{ user.email }}</li>
                        <li><strong>Age:</strong> {{ user.age }}</li>
                        <li><strong>Country:</strong> {{ user.country }}</li>
                        <li><strong>Subscription:</strong> {{ user.subscription }}</li>
                        <li><strong>Phone:</strong> {{ user.phone }}</li>
                      </ul>
                    </div>
                  </div>
                </div>
              </div>
              <div class="mt-5 sm:mt-6">
                <RouterLink
                  type="button"
                  class="mt-3 inline-flex w-full justify-center rounded-md bg-red-600 px-3 py-2 text-sm font-semibold text-white shadow-sm ring-1 ring-inset ring-red-700 hover:bg-red-500 sm:col-start-1 sm:mt-0"
                  to="/admin/users"
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

const user = ref({
  id: 1,
  first_name: "John",
  last_name: "Doe",
  email: "johndoe@gmail.com",
  password: "johndoe",
  age: 21,
  country: "Sri Lanka",
  subscription: "personal",
  phone: "+94777079697"
})

const users = ref([
  {
    id: 1,
    first_name: "John",
    last_name: "Doe",
    email: "johndoe@gmail.com",
    password: "johndoe",
    age: 21,
    country: "Sri Lanka",
    subscription: "personal",
    phone: "+94777079697"
  },
  {
    id: 2,
    first_name: "Jane",
    last_name: "Smith",
    email: "janesmith@gmail.com",
    password: "janesmith",
    age: 28,
    country: "USA",
    subscription: "family",
    phone: "+1234567890"
  },
  {
    id: 3,
    first_name: "David",
    last_name: "Brown",
    email: "davidbrown@gmail.com",
    password: "davidbrown",
    age: 35,
    country: "Canada",
    subscription: "business",
    phone: "+14161234567"
  },
  {
    id: 4,
    first_name: "Emily",
    last_name: "Davis",
    email: "emilydavis@gmail.com",
    password: "emilydavis",
    age: 30,
    country: "Australia",
    subscription: "group",
    phone: "+61412345678"
  },
  {
    id: 5,
    first_name: "Michael",
    last_name: "Wilson",
    email: "michaelwilson@gmail.com",
    password: "michaelwilson",
    age: 27,
    country: "UK",
    subscription: "personal",
    phone: "+447911123456"
  },
  {
    id: 6,
    first_name: "Sarah",
    last_name: "Taylor",
    email: "sarahtaylor@gmail.com",
    password: "sarahtaylor",
    age: 32,
    country: "New Zealand",
    subscription: "business",
    phone: "+64211234567"
  },
  {
    id: 7,
    first_name: "Chris",
    last_name: "Martinez",
    email: "chrismartinez@gmail.com",
    password: "chrismartinez",
    age: 24,
    country: "Spain",
    subscription: "personal",
    phone: "+34612345678"
  },
  {
    id: 8,
    first_name: "Laura",
    last_name: "Garcia",
    email: "lauragarcia@gmail.com",
    password: "lauragarcia",
    age: 29,
    country: "Mexico",
    subscription: "family",
    phone: "+521234567890"
  },
  {
    id: 9,
    first_name: "Robert",
    last_name: "Lee",
    email: "robertlee@gmail.com",
    password: "robertlee",
    age: 33,
    country: "South Korea",
    subscription: "group",
    phone: "+821012345678"
  },
  {
    id: 10,
    first_name: "Megan",
    last_name: "Harris",
    email: "meganharris@gmail.com",
    password: "meganharris",
    age: 26,
    country: "South Africa",
    subscription: "personal",
    phone: "+27123456789"
  }
])
</script>

<style></style>
