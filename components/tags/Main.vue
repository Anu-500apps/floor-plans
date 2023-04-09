<template>
  <div>
    <tagsAdd
      v-if="openModal"
      :open="openModal"
      @submit-tag="submitTags"
    ></tagsAdd>
    <tagsList
      :getTags="tags"
      @open-modal="openModal = true"
      @delete-row="deleleTagRow"
      @edit-row="editPrefill"
    ></tagsList>
    <tagsEdit
      :editForm="editForm"
      v-if="editModal"
      @update-tag="updateModal"
    ></tagsEdit>
  </div>
</template>
<script setup>
const openModal = ref(false);
const tags = ref([]);
const editForm = ref({ name: "" });
const editModal = ref(false);
const formIndex = ref(0);
// To get Bank Details
const getTagsData = () => {
  const { data: tagsResponse } = useAuthLazyFetch(
    "https://v1-orm-lib.mars.hipso.cc/api/tags/entity/CONTACTS?offset=0&limit=100&sort_column=id&sort_direction=desc"
  );
  tags.value = tagsResponse.value;
};
getTagsData();

// To submit form
const submitTags = async (formData: Object) => {
  let tagoptions = {
    body: formData,
  };
  const { data: storeTags } = await useAuthLazyFetchPost(
    "https://v1-orm-lib.mars.hipso.cc/api/tags/",
    tagoptions
  );
  tags.value.unshift(storeTags);
};

// To prefill form
const editPrefill = (tag: Object, index: Number) => {
  editForm.value = { ...tag };
  editModal.value = true;
};

// Update tag after edit
const updateModal = async (payload: Object) => {
  let editOptions = {
    body: payload
  };
  await useAuthLazyFetchPut(
    `https://v1-orm-lib.mars.hipso.cc/api/tags/${payload.uid}?name=${payload.name}`,
    editOptions
  );
};

// When delete tags at particular row on click
const deleleTagRow = async (deleteTag: Object, index: Number) => {
  await useAuthLazyFetchDelete(
    `https://v1-orm-lib.mars.hipso.cc/api/tags/${deleteTag.uid}`,""
  );
  tags.value.splice(index, 1);
};
</script>
