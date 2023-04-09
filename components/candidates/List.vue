<template>
  <div class="px-4 sm:px-6 lg:px-8">
    <!-- add button start -->
    <div class="sm:flex sm:items-center">
      <div class="sm:flex-auto font-serif">
        <h1 class="text-base font-semibold leading-6 text-gray-900">Candidates Details</h1>
        <p class="mt-2 text-sm text-gray-700">A list of all the Candidates</p>
      </div>
      <div class="mt-4 sm:ml-16 sm:mt-0 sm:flex-none">
        <button
          type="button"
          @click="emits('open-sidebar')"
          class="mt-2 block rounded-md bg-gray-600 px-3 py-2 text-center text-sm font-semibold text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600"
        >
          + Candidate
        </button>
      </div>
    </div>
    <!-- add button end -->
    <div class="mt-8 flow-root">
      <div class="-mx-4 -my-2 overflow-x-auto sm:-mx-6 lg:-mx-8">
        <div class="inline-block min-w-full py-2 align-middle sm:px-6 lg:px-8">
          <div
            class="overflow-hidden shadow ring-1 ring-black ring-opacity-5 sm:rounded-lg"
          >
            <!-- Candidates table start -->
            <table class="min-w-full divide-y divide-gray-300">
              <thead class="bg-blue-50">
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
                    Type
                  </th>
                  <th
                    scope="col"
                    class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900"
                  >
                    Due Date
                  </th>
                  <th
                    scope="col"
                    class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900"
                  >
                    Difficulty Level
                  </th>
                  <th
                    scope="col"
                    class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900"
                  >
                    Status
                  </th>
                  <th
                    scope="col"
                    class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900"
                  >
                    Multiple Attempts Allowed
                  </th>
                  <th scope="col" class="relative py-3.5 pl-3 pr-4 sm:pr-6">
                    <span class="sr-only">Edit</span>
                  </th>
                </tr>
              </thead>
              <tbody class="divide-y divide-gray-200 bg-white font-serif">
                <tr v-for="(candidatesData, index) in candidates" :key="index">
                  <td
                    class="whitespace-nowrap py-4 pl-4 pr-3 text-sm text-blue-900 font-black sm:pl-6"
                  >
                    {{ candidatesData.name }}
                  </td>
                  <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">
                    {{ candidatesData.type }}
                  </td>
                  <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">
                    {{ candidatesData.due_date }}
                  </td>
                  <td class="whitespace-nowrap px-3 py-4 text-sm text-blue-900">
                    {{ candidatesData.difficulty_level }}
                  </td>
                  <td class="whitespace-nowrap px-3 py-4 text-sm text-blue-500">
                    {{ candidatesData.status }}
                  </td>
                  <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">
                    {{ candidatesData.multiple_attempts_allowed }}
                  </td>
                </tr>
              </tbody>
            </table>
             <!-- Candidates table end -->
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
// Define Import Statements
import { ref, defineProps, defineEmits } from "vue";
import {
  Dialog,
  DialogPanel,
  DialogTitle,
  TransitionChild,
  TransitionRoot,
} from "@headlessui/vue";
import { ExclamationTriangleIcon } from "@heroicons/vue/24/outline";

const open = ref(false);
// Define Props
const props = defineProps({
  candidates: Array,
});
// Define Emits
const emits = defineEmits(["open-sidebar"]);
</script>
