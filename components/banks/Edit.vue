<template>
  <div class="flex">
    <PencilSquareIcon
      class="h-6 w-6 text-blue-700"
    ></PencilSquareIcon>
    <TrashIcon class="h-6 w-6 text-red-700" @click="emits('delete-row')"></TrashIcon>
  </div>
</template>
<script setup lang="ts">
// Define Import Statements
import { PencilSquareIcon, TrashIcon } from "@heroicons/vue/24/outline";
import {  defineEmits } from "vue";

// Define emits
const emits = defineEmits(["delete-row"]);

</script>
