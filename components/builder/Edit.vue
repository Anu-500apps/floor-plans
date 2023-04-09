<template>
  <!-- start edit sidebar -->
  <TransitionRoot as="template" :show="openSlideout">
    <Dialog as="div" class="relative z-10" @close="openSlideout = false">
      <div class="fixed inset-0 overflow-hidden">
        <div class="absolute inset-0 overflow-hidden">
          <div
            class="pointer-events-none fixed inset-y-0 right-0 flex max-w-full pl-10"
          >
            <TransitionChild
              as="template"
              enter="transform transition ease-in-out duration-500 sm:duration-700"
              enter-from="translate-x-full"
              enter-to="translate-x-0"
              leave="transform transition ease-in-out duration-500 sm:duration-700"
              leave-from="translate-x-0"
              leave-to="translate-x-full"
            >
              <DialogPanel class="pointer-events-auto w-screen max-w-md">
                <div
                  class="flex h-full flex-col overflow-y-scroll bg-white py-6 shadow-xl"
                >
                  <div class="px-4 sm:px-6">
                    <div class="flex items-start justify-between">
                      <DialogTitle
                        class="text-base font-semibold leading-6 text-gray-900"
                        >Edit Form</DialogTitle
                      >
                      <div class="ml-3 flex h-7 items-center">
                        <button
                          class="rounded-md bg-white text-gray-400 hover:text-gray-500 focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:ring-offset-2"
                          @click="openSlideout = false"
                        >
                          <span class="sr-only">Close panel</span>
                          <XMarkIcon class="h-6 w-6" aria-hidden="true" />
                        </button>
                      </div>
                    </div>
                  </div>
                  <!-- Start builder EditForm -->
                      <form>
                    <div
                      class="relative mt-6 flex-1 px-4 sm:px-6 border ml-2 mr-2"
                    >
                      <div class="mt-2">
                        <label
                          for="name"
                          class="block text-sm font-medium leading-6 text-gray-900"
                          > Name</label
                        >
                        <div class="mt-2">
                          <input
                            type="text"
                            id="name"
                            v-model="formPrefillData.name"
                            class="pl-2 block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
                            placeholder="Enter Name"
                          />
                        </div>
                      </div>
                      <div class="mt-2">
                        <label
                          for="number"
                          class="block text-sm font-medium leading-6 text-gray-900"
                          >Phone Number</label
                        >
                        <div class="mt-2">
                          <input
                            type="text"
                            id="number"
                            v-model="formPrefillData.phone_number"
                            class="pl-2 block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
                            placeholder="Enter Phone Number"
                          />
                        </div>
                      </div>

                      <div class="mt-2">
                        <label
                          for="email"
                          class="block text-sm font-medium leading-6 text-gray-900"
                          >Email</label
                        >
                        <div class="mt-2">
                          <input
                            type="text"
                            id="email"
                            v-model="formPrefillData.email"
                            class="pl-2 block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
                            placeholder="Enter Email"
                          />
                        </div>
                      </div>

                      <div class="mt-2">
                        <label
                          for="year"
                          class="block text-sm font-medium leading-6 text-gray-900"
                          >Established Year
                        </label>
                        <div class="mt-2">
                          <input
                            type="text"
                            id="year"
                            v-model="formPrefillData.established_year"
                            class="pl-2 block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
                            placeholder="Enter Established Year "
                          />
                        </div>
                      </div>
                      <div class="mt-2">
                        <div class="mt-2 mb-2 ml-[15.25rem] flex">
                          <div>
                            <button
                              @click="open = false"
                              class="mr-1 rounded bg-white px-2 py-1 text-sm font-semibold text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 hover:bg-gray-50"
                            >
                              Cancel
                            </button>
                          </div>
                          <div>
                          
                            <button
                              class="rounded bg-indigo-600 px-2 py-1 text-sm font-semibold text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600"
                              @click="updateBuilderDetails(), (open = false)"
                            >
                              Update
                            </button>
                          </div>
                        </div>
                      </div>
                    </div>
                  </form>
                  <!-- End builder EditForm -->
                </div>
              </DialogPanel>
            </TransitionChild>
          </div>
        </div>
      </div>
    </Dialog>
  </TransitionRoot>
  <!-- end edit sidebar -->
</template>
<script setup lang="ts">
// import Statements
import {
  Dialog,
  DialogPanel,
  DialogTitle,
  TransitionChild,
  TransitionRoot,
} from "@headlessui/vue";
import { XMarkIcon, PencilSquareIcon } from "@heroicons/vue/24/outline";
import { defineProps, defineEmits } from "vue";


// Define Props
const props = defineProps({
  openSlideout: Boolean,
  formPrefillData:Array
});


// Define Emits
const emits = defineEmits(["update-form-data"]);


// When edit form when user will click on update button
const updateBuilderDetails = () => {
   emits("update-form-data", props.formPrefillData);
};
</script>