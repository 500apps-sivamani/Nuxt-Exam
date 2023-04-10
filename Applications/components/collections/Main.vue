<template>
  <CollectionsList
    @createJobModalPopup="openModal"
    :getApplicationData="getCallData"
  />

  <div v-if="is_modal" :key="render">
    <CollectionsAdd @applicationBody="applicationPostData" />
  </div>
</template>
<script setup lang="ts">
const is_modal = ref(false);
const render = ref(0);

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
const getData = await useAuthLazyFetch(
  "https://v1-stark-db-orm.mars.hipso.cc/api/applications/?offset=0&limit=100",
  getOptions
);
const getCallData = ref("");
getCallData.value = getData.data._rawValue;

//POST Call for saving the Job Data
const applicationPostData = async (body: Object) => {
  const postOptions = {
    method: "POST",
    headers: authHeader,
    body: JSON.stringify(body),
  };
  await useAuthLazyFetchPost(
    "https://v1-stark-db-orm.mars.hipso.cc/api/applications/",
    postOptions
  );
  is_modal.value = false;
  getCallData.value.unshift(body);
};
</script>
