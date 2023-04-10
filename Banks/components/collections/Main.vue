<template>
  <CollectionsList
    @createExamModalPopup="openModal"
    :getBanksData="getBanksData"
  />

  <div v-if="is_modal" :key="render">
    <CollectionsAdd @banksBody="banksBodyPostCall" />
  </div>
</template>
<script setup lang="ts">
const is_modal = ref(false);
const render = ref(0);
const getBanksData = ref([]);

const openModal = () => {
  is_modal.value = true;
  render.value++;
};

//Declaring Authorization Header (Bearer Token)
const authHeader = {
  "Content-Type": "application/json",
  Authorization: `Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1IjoiNmZlZDJiYTgwYThkNGM0MjlhZGZiOGQ1ZTZmZTY0ODAiLCJkIjoiMTY4MDA4NCIsInIiOiJzYSIsInAiOiJmcmVlIiwiYSI6ImZpbmRlci5pbyIsImwiOiJ1czEiLCJleHAiOjE2ODMyNzk3Mjl9.5cJkrudAvTWoVRigTNcfQ321W_lOyMm-xsb9rMxuVBE`,
};

const getOptions = {
  method: "GET",
  headers: authHeader,
};

const getBankDetails = async () => {
  const { data: getData } = await useAuthLazyFetch(
    "https://v7-stark-db-orm.mercury.infinity-api.net/api/question-bank/?offset=0&limit=100&sort_column=id&sort_direction=desc",
    getOptions
  );
  getBanksData.value = getData.value;
};
getBankDetails();

//POST Call for saving the Job Data
const banksBodyPostCall = async (body: Object) => {
  const postOptions = {
    method: "POST",
    headers: authHeader,
    body: JSON.stringify(body),
  };
  await useAuthLazyFetchPost(
    "https://v7-stark-db-orm.mercury.infinity-api.net/api/question-bank/bulk",
    postOptions
  );
  is_modal.value = false;
  getBankDetails();
};
</script>
