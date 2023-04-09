<template>
  <CollectionsList
    :getBuilders="getBuildersData"
    @addBuilderSidebar="addBuilderSidebar"
    @editCall="openEditSidebar"
    @deleteCall="deleteBuilderData"
  />

  <div v-if="is_sidebar" :key="render">
    <CollectionsAdd @builderPostBody="builderPostCall" />
  </div>

  <div v-if="isEdit" :key="render">
    <CollectionsEdit
      @builderEditBody="builderEditCall"
      :prefillData="prefillData"
    />
  </div>
</template>

<script setup lang="ts">
const is_sidebar = ref(false);
const render = ref(0);
const isEdit = ref(false);
const prefillData = ref({});

//open customfields sidebar
const addBuilderSidebar = () => {
  is_sidebar.value = true;
  render.value++;
};

const openEditSidebar = (data: any) => {
  isEdit.value = true;
  render.value++;
  prefillData.value = { ...data };
  console.log("prefillData>>>>>>>>>>>>>>", prefillData.value);
};

const url = "https://v1-orm-gharpe.mercury.infinity-api.net/api/builder/";

//Declaring Authorization Header (Bearer Token)
const authHeader = {
  "Content-Type": "application/json",
  Authorization: `Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1IjoiNmZlZDJiYTgwYThkNGM0MjlhZGZiOGQ1ZTZmZTY0ODAiLCJkIjoiMTY4MDA4NCIsInIiOiJzYSIsInAiOiJmcmVlIiwiYSI6ImZpbmRlci5pbyIsImwiOiJ1czEiLCJleHAiOjE2ODMyNzk3Mjl9.5cJkrudAvTWoVRigTNcfQ321W_lOyMm-xsb9rMxuVBE`,
};

// Getting the customFields saved data through GET Call
const getOptions = {
  method: "GET",
  headers: authHeader,
};

const getData = await useAuthLazyFetch(
  "https://v1-orm-gharpe.mercury.infinity-api.net/api/builder/?offset=0&limit=100&sort_column=id&sort_direction=desc",
  getOptions
);
let getBuildersData = ref("");
getBuildersData.value = getData.data._rawValue;

//Saving the data through POST call (save)
const builderPostCall = async (body: Object) => {
  const options = {
    method: "POST",
    headers: authHeader,
    body: JSON.stringify(body),
  };
  await useAuthLazyFetchPost(`${url}`, options);

  //To display the data immediately on the UI
  getBuildersData.value.unshift(body);

  //immediately closing the sidebar after saving
  is_sidebar.value = false;
};

//Edit the builder Data PUT Call
const builderEditCall = async (body: Object) => {
  console.log("body", body);
  const editOptions = {
    method: "PUT",
    headers: authHeader,
    body: JSON.stringify(body),
  };

  await useAuthLazyFetchPut(`${url}${body.uid}`, editOptions);
  isEdit.value = false;
};

// Delete Call
const deleteBuilderData = async (data: any) => {
  console.log("data-->.", data.uid);
  const deleteOptions = {
    method: "DELETE",
    headers: authHeader,
  };
  await useAuthLazyFetchDelete(
    `https://v1-orm-gharpe.mercury.infinity-api.net/api/builder/${data.uid}`,
    deleteOptions
  );
  getBuildersData.value.forEach((item: any, index: any) => {
    if (item.uid === data.uid) {
      getBuildersData.value.splice(index, 1);
    }
  });
};
</script>
