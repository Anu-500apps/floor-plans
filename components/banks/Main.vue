<template>
  <div>
    <banksList
      @open-sidebar="openSidebar = true"
      :bankDetails="bankDetails"
      :openSlideout="openSidebar"
    ></banksList>
    <banksAdd
      v-if="openSidebar"
      :open="openSidebar"
      @submit-bank-data="submitBankData"
    ></banksAdd>
  </div>
</template>
<script setup lang="ts">
// import statements
import { ref } from "vue";
const openSidebar = ref(false);
const bankDetails = ref([]);

// To get Bank Details
const { data: getbankDetails } = await useAuthLazyFetch(
  "https://v7-stark-db-orm.mercury.infinity-api.net/api/question-bank/?offset=0&limit=100&sort_column=id&sort_direction=desc"
);
bankDetails.value = getbankDetails.value;

// To submit form data when click on submit button
const submitBankData = async (formData: Object) => {
  let options = {
    body: [formData],
  };
  const { data: storeFormData } = await useAuthLazyFetchPost(
    "https://v7-stark-db-orm.mercury.infinity-api.net/api/question-bank/bulk",
    options
  );
  bankDetails.value.unshift(storeFormData);
};
</script>
