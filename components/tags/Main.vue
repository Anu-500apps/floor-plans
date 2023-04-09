<template>
  <div>
    <tagsAdd v-if="openModal" :open="open" @submit-tag="submitTags"></tagsAdd>
    <tagsList :getTags="tags" @open-modal="openModal = true"></tagsList>
  </div>
</template>
<script setup>
import { PlusIcon } from "@heroicons/vue/20/solid";
const openModal = ref(false);
const tags = ref([]);
// To get Bank Details
const getTagsData = async () => {
  const { data: getTags } = await useAuthLazyFetch(
    "https://v1-orm-lib.mars.hipso.cc/api/tags/entity/CONTACTS?offset=0&limit=100&sort_column=id&sort_direction=desc"
  );
  tags.value = getTags.value;
};
getTagsData();

const submitTags = async (formData) => {
  let tagoptions = {
    body: formData,
  };
  const { data: storeTags } = await useAuthLazyFetchPost(
    "https://v1-orm-lib.mars.hipso.cc/api/tags/",
    tagoptions
  );
  // getTagsData();
  tags.value = storeTags.value;
};
</script>
