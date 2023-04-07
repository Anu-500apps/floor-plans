<template>
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
                Name
              </th>
              <th
                scope="col"
                class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900"
              >
                Facing
              </th>
              <th
                scope="col"
                class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900"
              >
                Metric Name
              </th>
              <th
                scope="col"
                class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900"
              >
                Kitchens
              </th>
              <th scope="col" class="relative py-3.5 pl-3 pr-4 sm:pr-0">
                <span class="sr-only">Edit</span>
              </th>
            </tr>
          </thead>
          <tbody class="divide-y divide-gray-200">
            <tr v-for="(floorPlans, index) in formData" :key="floorPlans.name">
              <td
                class="whitespace-nowrap py-4 pl-4 pr-3 text-sm font-medium text-gray-900 sm:pl-0"
              >
                {{ floorPlans.name }}
              </td>
              <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">
                {{ floorPlans.facing }}
              </td>
              <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">
                {{ floorPlans.metric_name }}
              </td>
              <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">
                {{ floorPlans.kitchens }}
              </td>
              <td
                class="relative whitespace-nowrap py-4 pl-3 pr-4 text-right text-sm font-medium sm:pr-0"
              >
                <button
                  class="text-indigo-600 hover:text-indigo-900"
                  @click="emits('edit-form', floorPlans, index)"
                >
                  Edit
                </button>
              </td>
              <td
                class="relative whitespace-nowrap py-4 pl-3 pr-4 text-right text-sm font-medium sm:pr-0"
              >
                <button
                  href="#"
                  class="text-indigo-600 hover:text-indigo-900"
                  @click="open = true"
                >
                  Delete<span class="sr-only"></span>
                </button>
              </td>
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
                    <div
                      class="fixed inset-0 bg-gray-500 bg-opacity-75 transition-opacity"
                    />
                  </TransitionChild>

                  <div class="fixed inset-0 z-10 overflow-y-auto">
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
                          class="relative transform overflow-hidden rounded-lg bg-white px-4 pb-4 pt-5 text-left shadow-xl transition-all sm:my-8 sm:w-full sm:max-w-lg sm:p-6"
                        >
                          <div class="sm:flex sm:items-start">
                            <div
                              class="mx-auto flex h-12 w-12 flex-shrink-0 items-center justify-center rounded-full bg-red-100 sm:mx-0 sm:h-10 sm:w-10"
                            >
                              <ExclamationTriangleIcon
                                class="h-6 w-6 text-red-600"
                                aria-hidden="true"
                              />
                            </div>
                            <div
                              class="mt-3 text-center sm:ml-4 sm:mt-0 sm:text-left"
                            >
                              <DialogTitle
                                as="h3"
                                class="text-base font-semibold leading-6 text-gray-900"
                                >Are you sure ?</DialogTitle
                              >
                              <div class="mt-2">
                                <p class="text-sm text-gray-500">
                                  Deleting will permanently remove. This cannot
                                  be undone.
                                </p>
                              </div>
                            </div>
                          </div>
                          <div class="mt-5 sm:ml-10 sm:mt-4 sm:flex sm:pl-4">
                            <button
                              type="button"
                              class="inline-flex w-full justify-center rounded-md bg-red-600 px-3 py-2 text-sm font-semibold text-white shadow-sm hover:bg-red-500 sm:w-auto"
                              @click="
                                emits('delete-form', floorPlans), (open = false)
                              "
                            >
                              Delete
                            </button>
                            <button
                              type="button"
                              class="mt-3 inline-flex w-full justify-center rounded-md bg-white px-3 py-2 text-sm font-semibold text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 hover:bg-gray-50 sm:ml-3 sm:mt-0 sm:w-auto"
                              @click="open = false"
                              ref="cancelButtonRef"
                            >
                              Cancel
                            </button>
                          </div>
                        </DialogPanel>
                      </TransitionChild>
                    </div>
                  </div>
                </Dialog>
              </TransitionRoot>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>
<script setup lang="ts">
import { ref } from "vue";
import {
  Dialog,
  DialogPanel,
  DialogTitle,
  TransitionChild,
  TransitionRoot,
} from "@headlessui/vue";
import { ExclamationTriangleIcon } from "@heroicons/vue/24/outline";
import { defineEmits } from "vue";
const open = ref(false);
// Declare Emits here
const emits = defineEmits(["edit-form", "delete-form"]);
const props = defineProps({
  // Declare props
  formData: Object,
});
</script>
