<template>
  <CollectionsList
    :projectsGetData="projectsGetData"
    @openProjectSideBar="openProjectSideBar"
    @editCall="editprojectsData"
    @deleteCall="deleteProjectsData"
  />

  <div v-if="is_sidebar" :key="render">
    <CollectionsAdd @projectsBody="projectsBodyPostCall" />
  </div>

  <div v-if="isEdit" :key="render">
    <CollectionsEdit @projectsPutBody="projectsPutCall" :editProp="editProp" />
  </div>
</template>

<script setup lang="ts">
//open customfields sidebar
const is_sidebar = ref(false);
const render = ref(0);
const isEdit = ref(false);
const editProp = ref({});

const openProjectSideBar = () => {
  is_sidebar.value = true;
  render.value++;
};
const editprojectsData = (data: any) => {
  isEdit.value = true;
  render.value++;
  editProp.value = data;
};

const url = "https://v1-orm-gharpe.mercury.infinity-api.net/api/projects/";

//Declaring Authorization Header (Bearer Token)
const authHeader = {
  "Content-Type": "application/json",
  Authorization: `Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1IjoiNmZlZDJiYTgwYThkNGM0MjlhZGZiOGQ1ZTZmZTY0ODAiLCJkIjoiMTY4MDA4NCIsInIiOiJzYSIsInAiOiJmcmVlIiwiYSI6ImZpbmRlci5pbyIsImwiOiJ1czEiLCJleHAiOjE2ODMyNzk3Mjl9.5cJkrudAvTWoVRigTNcfQ321W_lOyMm-xsb9rMxuVBE`,
};

// Getting the projects Data saved data through GET Call
const getOptions = {
  method: "GET",
  headers: authHeader,
};
const getData = await useAuthLazyFetch(
  "https://v1-orm-gharpe.mercury.infinity-api.net/api/projects/?offset=0&limit=100&sort_column=id&sort_direction=desc",
  getOptions
);
const projectsGetData = ref("");
projectsGetData.value = getData.data._rawValue;

//Saving the data through POST call (save)
const projectsBodyPostCall = async (body: Object) => {
  const options = {
    method: "POST",
    headers: authHeader,
    body: JSON.stringify(body),
  };
  await useAuthLazyFetchPost(`${url}`, options);

  //To display the data immediately on the UI
  projectsGetData.value.unshift(body);

  //immediately closing the sidebar after saving
  is_sidebar.value = false;
};

//Edit the Projects Data PUT Call
const projectsPutCall = async (body: any) => {
  const editOptions = {
    method: "PUT",
    headers: authHeader,
    body: JSON.stringify(body),
  };

  await useAuthLazyFetchPut(`${url}${body.uid}`, editOptions);
  isEdit.value = false;
};

//Delete Call
const deleteProjectsData = async (data: any) => {
  const deleteOptions = {
    method: "DELETE",
    headers: authHeader,
  };
  await useAuthLazyFetchDelete(
    `https://v1-orm-gharpe.mercury.infinity-api.net/api/projects/${data.uid}`,
    deleteOptions
  );
  projectsGetData.value.forEach((item: any, index: any) => {
    if (item.uid === data.uid) {
      projectsGetData.value.splice(index, 1);
    }
  });
};
console.log("projectsGetDataAfterrrrr===>", projectsGetData.value);
</script>
