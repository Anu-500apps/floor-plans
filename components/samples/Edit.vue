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
                        >Edit Project</DialogTitle
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
                  <!-- Start Projects EditForm -->
                  <form>
                    <div
                      class="relative mt-6 flex-1 px-4 sm:px-6 border ml-2 mr-2"
                    >
                      <div class="mt-2">
                        <label
                          for="category"
                          class="block text-sm font-medium leading-6 text-gray-900"
                          >Project Name</label
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
                          for="list"
                          class="block text-sm font-medium leading-6 text-gray-900"
                          >List Type</label
                        >
                        <div class="mt-2">
                          <input
                            type="text"
                            id="list type"
                            v-model="formPrefillData.listing_type_name"
                            class="pl-2 block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
                            placeholder="Enter List type"
                          />
                        </div>
                      </div>

                      <div class="mt-2">
                        <label
                          for="details"
                          class="block text-sm font-medium leading-6 text-gray-900"
                          >Details</label
                        >
                        <div class="mt-2">
                          <input
                            type="text"
                            id="question"
                            v-model="formPrefillData.details"
                            class="pl-2 block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
                            placeholder="Enter Details"
                          />
                        </div>
                      </div>

                      <div class="mt-2">
                        <label
                          for="specifications"
                          class="block text-sm font-medium leading-6 text-gray-900"
                          >Specifications
                        </label>
                        <div class="mt-2">
                          <input
                            type="text"
                            id="specifications"
                            v-model="formPrefillData.specifications"
                            class="pl-2 block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
                            placeholder="Enter Specifications "
                          />
                        </div>
                      </div>
                      <div class="mt-2">
                        <label
                          for="approve_status"
                          class="block text-sm font-medium leading-6 text-gray-900"
                          >Approve Status</label
                        >
                        <div class="mt-2">
                          <input
                            id="approve_status"
                            v-model="formPrefillData.approve_status"
                            class="pl-2 block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
                            placeholder="Enter Status"
                          />
                        </div>
                      </div>
                      <div class="mt-2">
                        <label
                          for="age_of_projects"
                          class="block text-sm font-medium leading-6 text-gray-900"
                          >Age Of Projects</label
                        >
                        <div class="mt-2">
                          <input
                            type="text"
                            id="age_of_projects"
                            v-model="formPrefillData.age_of_the_project"
                            class="pl-2 block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
                            placeholder="Enter Age Of Projects"
                          />
                        </div>
                      </div>

                      <div class="mt-2">
                        <label
                          for="total_projects"
                          class="block text-sm font-medium leading-6 text-gray-900"
                          >Total Project Area</label
                        >
                        <div class="mt-2">
                          <input
                            id="total_projects"
                            type="number"
                            v-model="formPrefillData.total_project_area"
                            class="pl-2 block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
                            placeholder="Enter Total Projects"
                          />
                        </div>
                      </div>
                      <div class="mt-2">
                        <div class="mt-2 mb-2 ml-[15.25rem] flex">
                          <div>
                            <button
                              @click="openSlideout = false"
                              class="mr-1 rounded bg-white px-2 py-1 text-sm font-semibold text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 hover:bg-gray-50"
                            >
                              Cancel
                            </button>
                          </div>
                          <div>
                          
                            <button
                              class="rounded bg-indigo-600 px-2 py-1 text-sm font-semibold text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600"
                              @click="updateProjectForm(), (openSlideout = false)"
                            >
                              Update
                            </button>
                          </div>
                        </div>
                      </div>
                    </div>
                  </form>
                  <!-- End Projects EditForm -->
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
const updateProjectForm = () => {
   emits("update-form-data", props.formPrefillData);
};
</script>
