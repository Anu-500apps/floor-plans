<template>
  <div>
    <candidatesList
      @open-sidebar="openSidebar = true"
      :candidates="candidates"
    ></candidatesList>
    <candidatesAdd
      v-if="openSidebar"
      :open="openSidebar"
      @send-details="sendCandidatesDetails"
    ></candidatesAdd>
  </div>
</template>
<script setup lang="ts">
// import statements
import { ref } from "vue";
const openSidebar = ref(false);
const candidates = ref([]);

// To get Candidtes Details
const getCandidates = async () => {
  const { data: getResponse } = await useAuthLazyFetch(
    "https://v7-stark-db-orm.mercury.infinity-api.net/api/mock-interviews/?offset=0&limit=100&sort_column=id&sort_direction=desc"
  );
  candidates.value = getResponse.value;
};
getCandidates();

// To submit form data when click on submit button
const sendCandidatesDetails = async (body: Object) => {
  let options = {
    body: body,
  };
  const { data: responseData } = await useAuthLazyFetchPost(
    "https://v7-stark-db-orm.mercury.infinity-api.net/api/mock-interviews/",
    options
  );
  candidates.value.unshift(responseData.value);
};
</script>
