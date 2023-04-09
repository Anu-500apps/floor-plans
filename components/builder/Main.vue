<template>
  <div>
    <builderList
      @open-sidebar-form="openSidebar = true"
      :buildersDetails="buildersDetails"
      @edit-row="editPrefill"
      :openSlideout="openSidebar"
      @delete-row="deleteRow"
    ></builderList>
    <builderAdd
      v-if="openSidebar"
      :open="openSidebar"
      @submit-form-data="submitFormData"
    ></builderAdd>
    <builderEdit
      v-if="editSlidebar"
      :openSlideout="editSlidebar"
      @submit-form-data="submitFormData"
      :formPrefillData="formPrefillData"
      @update-form-data="updateForm"
    ></builderEdit>
  </div>
</template>
<script setup lang="ts">
// import statements
import { ref } from "vue";

const openSidebar = ref(false);
const buildersDetails = ref([]);
const editSlidebar = ref(false);
const formPrefillData = ref({});

// To get builders Details
const { data: getbuildersDetails } = useAuthLazyFetch(
  "https://v1-orm-gharpe.mercury.infinity-api.net/api/builder/?offset=0&limit=100&sort_column=id&sort_direction=desc"
);
buildersDetails.value = getbuildersDetails.value;

// To submit form data when click on submit button
const submitFormData = async (body: Object) => {
  let options = {
    body: body,
  };
  const { data: response } = await useAuthLazyFetchPost(
    "https://v1-orm-gharpe.mercury.infinity-api.net/api/builder/",
    options
  );
  buildersDetails.value.unshift(response);
};

// when click on edit button then form is autofill
const editPrefill = (editForm: Object) => {
  formPrefillData.value = { ...editForm };
  editSlidebar.value = true;
};

// When update form data click on update button
const updateForm = async (builder: Object) => {
  let editOptions = {
    body:builder
  }
  await useAuthLazyFetchPut(
    `https://v1-orm-gharpe.mercury.infinity-api.net/api/builder/${builder.uid}`,
    editOptions
  );
};

// When delete data at particular row on click
const deleteRow = async (builder: Object, index:Number) => {
  await useAuthLazyFetchDelete(
    `https://v1-orm-gharpe.mercury.infinity-api.net/api/builder/${builder.uid}`,
    ""
  );
  buildersDetails.value.splice(index, 1);
};
</script>
