<template>
  <div class="px-4 sm:px-6 lg:px-8">
    <div class="sm:flex sm:items-center font-extrabold font-mono">
      <div class="sm:flex-auto">
        <h1 class="text-base font-semibold leading-6 text-gray-900">
          Builders
        </h1>
        <p class="mt-2 text-sm text-gray-700">A list of all the Builders</p>
      </div>
      <div class="mt-4 sm:ml-16 sm:mt-0 sm:flex-none ">
        <button
          type="button"
          class="block rounded-md bg-gray-600 px-3 py-2 text-center text-sm font-semibold text-white shadow-sm hover:bg-gray-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600"
          @click="emits('open-sidebar-form')"
        >
          Add Builder
        </button>
      </div>
    </div>
    <div class="mt-8 flow-root">
      <div class="-mx-4 -my-2 overflow-x-auto sm:-mx-6 lg:-mx-8">
        <div class="inline-block min-w-full py-2 align-middle sm:px-6 lg:px-8">
          <div
            class="overflow-hidden shadow ring-1 ring-black ring-opacity-5 sm:rounded-lg"
          >
            <!-- builder table start -->
            <table class="min-w-full divide-y divide-gray-300 font-extrabold font-mono">
              <thead class="bg-gray-500">
                <tr>
                  <th
                    scope="col"
                    class="py-3.5 pl-4 pr-3 text-left text-sm font-semibold text-gray-900 sm:pl-6"
                  >
                    Name
                  </th>
                  <th
                    scope="col"
                    class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900"
                  >
                    Phone Numbers
                  </th>
                  <th
                    scope="col"
                    class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900"
                  >
                    Email
                  </th>
                  <th
                    scope="col"
                    class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900"
                  >
                    Established Year
                  </th>
                  <th
                    scope="col"
                    class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900"
                  >
                    logo
                  </th>
                  <th
                    scope="col"
                    class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900"
                  >
                    Tag Line
                  </th>
                  <th scope="col" class="relative py-3.5 pl-3 pr-4 sm:pr-6">
                    <span class="sr-only">Edit</span>
                  </th>
                </tr>
              </thead>
              <tbody class="divide-y divide-gray-200 bg-white">
                <tr v-for="(builder, index) in buildersDetails" :key="index">
                  <td
                    class="whitespace-nowrap py-4 pl-4 pr-3 text-sm font-medium text-gray-900 sm:pl-6"
                  >
                    {{ builder.name }}
                  </td>
                  <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">
                    {{ builder.phone_number }}
                  </td>
                  <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">
                    {{ builder.email }}
                  </td>
                  <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">
                    {{ builder.established_year }}
                  </td>
                  <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">
                    {{ builder.logo }}
                  </td>
                  <td
                    class="whitespace-nowrap px-3 py-4 text-sm text-gray-500"
                  >
                    {{ builder.tag_line }}
                  </td>
                  <td
                    class="relative whitespace-nowrap py-4 pl-3 pr-4 text-right text-sm font-medium sm:pr-6"
                  >
                    <div class="flex">
                      <PencilSquareIcon
                        class="h-6 w-6 text-blue-700"
                        @click="emits('edit-row', builder)"
                      ></PencilSquareIcon>
                      <TrashIcon
                        class="h-6 w-6 text-red-700"
                        @click="emits('delete-row', builder,index)"
                      ></TrashIcon>
                    </div>
                  </td>
                </tr>
              </tbody>
            </table>
            <!-- builder table start -->
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
// Define Import Statements
import { PencilSquareIcon, TrashIcon } from "@heroicons/vue/24/outline";
import { ref, defineProps, defineEmits } from "vue";
import {
  Dialog,
  DialogPanel,
  DialogTitle,
  TransitionChild,
  TransitionRoot,
} from "@headlessui/vue";

const open = ref(false);
// Define Props
const props = defineProps({
  buildersDetails: Array,
});
// Define Emits
const emits = defineEmits(["open-sidebar-form","delete-row","edit-row",]);
</script>
