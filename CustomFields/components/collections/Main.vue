<template>
  <CollectionsList
    :getCustomData="getCustomData"
    @open-customfield-sidebar="openCustomField"
    @editCall="editCustomDataList"
    @deleteCall="deleteCustomData"
  />

  <div v-if="is_sidebar" :key="render">
    <CollectionsAdd @customPostBody="customBodyPostCall" />
  </div>

  <div v-if="isEdit" :key="render">
    <CollectionsEdit @customPutemit="customPutCall" :data="datatest" />
  </div>
</template>

<script setup lang="ts">
//open customfields sidebar
const is_sidebar = ref(false);
const render = ref(0);
const isEdit = ref(false);

const openCustomField = () => {
  is_sidebar.value = true;
  render.value++;
};

const url = "https://v1-orm-lib.mars.hipso.cc/api/custom-fields/";

//Declaring Authorization Header (Bearer Token)
const authHeader = {
  "Content-Type": "application/json",
  Authorization: `Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1IjoiNmZlZDJiYTgwYThkNGM0MjlhZGZiOGQ1ZTZmZTY0ODAiLCJkIjoiMTY4MDA4NCIsInIiOiJzYSIsInAiOiJmcmVlIiwiYSI6ImZpbmRlci5pbyIsImwiOiJ1czEiLCJleHAiOjE2ODMyNzk3Mjl9.5cJkrudAvTWoVRigTNcfQ321W_lOyMm-xsb9rMxuVBE`,
};

//Getting the customFields saved data through GET Call
const getOptions = {
  method: "GET",
  headers: authHeader,
};
const datatest = ref({});
const getData = await useAuthLazyFetch(
  "https://v1-orm-lib.mars.hipso.cc/api/custom-fields/CONTACTS?offset=0&limit=100&sort_column=id&sort_direction=desc",
  getOptions
);
let getCustomData = ref(getData.data._rawValue);

//Saving the data through POST call (save)
const customBodyPostCall = async (body: Object) => {
  const options = {
    method: "POST",
    headers: authHeader,
    body: JSON.stringify(body),
  };
  await useAuthLazyFetchPost(`${url}`, options);

  //To display the data immediately on the UI
  getCustomData.value.unshift(body);

  //immediately closing the sidebar after saving
  is_sidebar.value = false;
};

const editCustomDataList = (data: any) => {
  isEdit.value = true;
  render.value++;
  datatest.value = data;
};

//Edit the Custom Data PUT Call
const customPutCall = async (body: Object) => {
  const editOptions = {
    method: "PUT",
    headers: authHeader,
    body: JSON.stringify(body),
  };

  await useAuthLazyFetchPut(`${url}${body.uid}`, editOptions);
  isEdit.value = false;
};

//Delete Call
const deleteCustomData = async (data: object) => {
  const deleteOptions = {
    method: "DELETE",
    headers: authHeader,
  };
  await useAuthLazyFetchDelete(
    `https://v1-orm-lib.mars.hipso.cc/api/custom-fields/${data.uid}`,
    deleteOptions
  );
  getCustomData.value.shift(data);
};
</script>
