<template>
  <div>
    <samplesList
      @open-sidebar-form="openSidebar = true"
      :projectsData="projectsData"
      @edit-project-data="editPrefill"
      :openSlideout="openSidebar"
      @delete-project-data="deleteProject"
    ></samplesList>
    <samplesAdd
      v-if="openSidebar"
      :open="openSidebar"
      @submit-form-data="submitFormData"
    ></samplesAdd>
    <samplesEdit
      v-if="editSlidebar"
      :openSlideout="editSlidebar"
      @submit-form-data="submitFormData"
      :formPrefillData="formPrefillData"
      @update-form-data="updateForm"
    ></samplesEdit>
  </div>
</template>
<script setup lang="ts">
// import statements
import { ref } from "vue";
const openSidebar = ref(false);
const projectsData = ref([]);
const editSlidebar = ref(false);
const projectsIndex = ref(0);
const formPrefillData = ref({});

// To get Project Details
const getProjects = () => {
  const { data: getProjectsData } = useAuthLazyFetch(
    "https://v1-orm-gharpe.mercury.infinity-api.net/api/projects/?offset=0&limit=100&sort_column=id&sort_direction=desc"
  );
  projectsData.value = getProjectsData.value;
};
// To submit form data when click on submit button
const submitFormData = async (formData: Object) => {
  let options = {
    body: formData,
  };
  const { data: storeFormData } = await useAuthLazyFetchPost(
    "https://v1-orm-gharpe.mercury.infinity-api.net/api/projects/",
    options
  );
  projectsData.value.unshift(storeFormData);
};

// when click on edit button then form is autofill
const editPrefill = (editForm: Object) => {
  formPrefillData.value = { ...editForm };
  editSlidebar.value = true;
};

// When update form data click on update button
const updateForm = async (formDetails: Object) => {
  let options = { body: formDetails };
  const prefillForm = await useAuthLazyFetchPut(
    `https://v1-orm-gharpe.mercury.infinity-api.net/api/projects/${formDetails.uid}`,
    options
  );
  getProjects();
};

// When delete project at particular row on click
const deleteProject = async (project: Object) => {
  const options = { body: project };
  await useAuthLazyFetchDelete(
    `https://v1-orm-gharpe.mercury.infinity-api.net/api/projects/${project.uid}`,
    options
  );
  getProjects();
};
getProjects();
</script>
