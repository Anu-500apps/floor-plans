<template>
  <div class="px-4 sm:px-6 lg:px-8">
    <div class="sm:flex sm:items-center">
      <div class="mt-4 sm:flex">
        <button
          class="block rounded-md bg-indigo-600 px-3 py-2 text-center text-sm font-semibold text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600"
          @click="show = true"
        >
          Add
        </button>
      </div>
    </div>
    <collectionList
      :formData="formData"
      @edit-form="editPrefill"
      @delete-form="deleteData"
      :response="response"
    ></collectionList>
    <collectionAdd
      v-if="show"
      @submit-form="submitForm"
      :formsData="formsData"
    ></collectionAdd>
  </div>
</template>

<script setup>
const show = ref(false);
const formsData = ref({
  name: "",
  facing: "East",
  metric_name: "",
  kitchens: Number,
});
const formIndex = ref(0);

// Get data
const { data: formData } = await useAuthLazyFetch(
  "https://v1-orm-gharpe.mercury.infinity-api.net/api/floorplans/?offset=0&limit=100&sort_column=id&sort_direction=desc"
);

// For submit form
const submitForm = async (form) => {
  if (form.uid) updateForm(form);
  let options = {
    body: form,
  };
  const { data: addFormData } = await useAuthLazyFetchPost(
    "https://v1-orm-gharpe.mercury.infinity-api.net/api/floorplans/",
    options
  );
  form.value = {};
  formData.value.unshift(form);

};
const editPrefill = (floorPlans) => {
  formsData.value = { ...floorPlans };
  show.value = true;
};
// Updates Form after edit
const updateForm = async (form) => {
  let options = {
    body: form,
  };
  const { data: addTemplateData } = await useAuthLazyFetchPut(
    `https://v1-orm-gharpe.mercury.infinity-api.net/api/floorplans/${form.uid}`,
    options
  );
  formsData.value[formIndex.value] = form;
};
// Delete particular row
const deleteData = async () => {
  // There is no uid in ORM
  await useAuthLazyFetchDelete(
    `https://v1-orm-gharpe.mercury.infinity-api.net/api/floorplans/3fa85f64-5717-4562-b3fc-2c963f66afa6`
  );
  formsData.value.splice(index, 1);
};
</script>
