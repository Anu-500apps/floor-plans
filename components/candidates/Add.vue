<template>
  <!-- start addform sidebar -->
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
              class="relative transform overflow-hidden rounded-lg bg-white px-4 pb-4 pt-5 text-left shadow-xl transition-all sm:my-8 sm:w-full sm:max-w-sm sm:p-6"
            >
              <!-- Start candidates Form -->
              <form>
                <div class="relative mt-6 flex-1 px-4 sm:px-6 border ml-2 mr-2">
                  <div class="mt-2">
                    <label
                      for="name"
                      class="block text-sm font-medium leading-6 text-gray-900"
                      >Name</label
                    >
                    <div class="mt-2">
                      <input
                        type="name"
                        id="name"
                        v-model="form.name"
                        class="pl-2 block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
                        placeholder="Enter Name"
                      />
                    </div>
                  </div>
                  <div class="mt-2">
                    <label
                      for="type"
                      class="block text-sm font-medium leading-6 text-gray-900"
                      >Type</label
                    >
                    <div class="mt-2">
                      <input
                        type="text"
                        id="type"
                        v-model="form.type"
                        class="pl-2 block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
                        placeholder="Enter Type"
                      />
                    </div>
                  </div>

                  <div class="mt-2">
                    <label
                      for="date"
                      class="block text-sm font-medium leading-6 text-gray-900"
                      >Due Date</label
                    >
                    <div class="mt-2">
                      <input
                        type="date"
                        id="date"
                        v-model="form.due_date"
                        class="pl-2 block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
                      />
                    </div>
                  </div>
                  <div class="mt-2">
                    <label
                      for="level"
                      class="block text-sm font-medium leading-6 text-gray-900"
                    >
                      Difficulty Level
                    </label>
                    <div class="mt-2">
                      <input
                        type="text"
                        id="level"
                        v-model="form.difficulty_level"
                        class="pl-2 block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
                      />
                    </div>
                  </div>
                  <div class="mt-2">
                    <label
                      for="description"
                      class="block text-sm font-medium leading-6 text-gray-900"
                      >Description</label
                    >
                    <div class="mt-2">
                      <input
                        id="description"
                        v-model="form.description"
                        class="pl-2 block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
                        placeholder="Enter Description"
                      />
                    </div>
                  </div>
                  <div class="mt-2">
                    <div class="mt-2 mb-2 ml-[9.25rem] flex">
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
                          @click="sendCandidatesDetails(), (open = false)"
                        >
                          Submit
                        </button>
                      </div>
                    </div>
                  </div>
                </div>
              </form>
              <!-- End Bank Form -->
            </DialogPanel>
          </TransitionChild>
        </div>
      </div>
    </Dialog>
  </TransitionRoot>
  <!-- end addform sidebar -->
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
import { ref, defineProps, defineEmits } from "vue";
// Define Props
const props = defineProps({
  open: Boolean,
});
// Define Emits
const emits = defineEmits(["send-details"]);
const form = ref({
  name: "",
  type: "practice",
  max_time_allowed: 0,
  due_date: "2023-09-09T05:36:41.067Z",
  difficulty_level: "Easy",
  description: "",
  questions: {},
  multiple_attempts_allowed: 0,
  instructions: {},
  status: 0,
});

// To submit form when user will click on submit button
const sendCandidatesDetails = () => {
  emits("send-details", form.value);
};
</script>
