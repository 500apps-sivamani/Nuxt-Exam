<template>
  <div class="bg-gray-900 py-10">
    <div class="px-4 sm:px-6 lg:px-8">
      <div class="sm:flex sm:items-center">
        <div class="sm:flex-auto">
          <h1 class="text-base font-semibold leading-6 text-white">
            Add Projects
          </h1>
          <p class="mt-2 text-sm text-gray-300">
            You can add projects By click on "Add Projects"
          </p>
        </div>
        <div class="mt-4 sm:ml-16 sm:mt-0 sm:flex-none">
          <button
            @click="addProjects"
            type="button"
            class="block rounded-md bg-indigo-500 px-3 py-2 text-center text-sm font-semibold text-white hover:bg-indigo-400 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-500"
          >
            Add Projects
          </button>
        </div>
      </div>
      <div class="mt-8 flow-root">
        <div class="-mx-4 -my-2 overflow-x-auto sm:-mx-6 lg:-mx-8">
          <div
            class="inline-block min-w-full py-2 align-middle sm:px-6 lg:px-8"
          >
            <table class="min-w-full divide-y divide-gray-700">
              <thead>
                <tr>
                  <th
                    scope="col"
                    class="py-3.5 pl-4 pr-3 text-left text-sm font-semibold text-white sm:pl-0"
                  >
                    Project Name
                  </th>
                  <th
                    scope="col"
                    class="px-3 py-3.5 text-left text-sm font-semibold text-white"
                  >
                    Category
                  </th>
                  <th
                    scope="col"
                    class="px-3 py-3.5 text-left text-sm font-semibold text-white"
                  >
                    Sub Category
                  </th>
                  <th
                    scope="col"
                    class="px-3 py-3.5 text-left text-sm font-semibold text-white"
                  >
                    Status
                  </th>
                  <th
                    scope="col"
                    class="px-3 py-3.5 text-left text-sm font-semibold text-white"
                  >
                    Metric
                  </th>
                  <th
                    scope="col"
                    class="px-3 py-3.5 text-left text-sm font-semibold text-white"
                  >
                    Approve Status
                  </th>
                </tr>
              </thead>
              <tbody class="divide-y divide-gray-800">
                <tr
                  v-for="(projectsData, index) in projectsGetData"
                  :key="index"
                >
                  <td
                    class="whitespace-nowrap py-4 pl-4 pr-3 text-sm font-medium text-white sm:pl-0"
                  >
                    {{ projectsData.name }}
                  </td>
                  <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-300">
                    {{ projectsData.category }}
                  </td>
                  <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-300">
                    {{ projectsData.sub_category }}
                  </td>
                  <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-300">
                    {{ projectsData.status }}
                  </td>
                  <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-300">
                    {{ projectsData.metric }}
                  </td>
                  <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-300">
                    {{ projectsData.approve_status }}
                  </td>
                  <td
                    class="relative whitespace-nowrap py-4 pl-3 pr-4 text-right text-sm font-medium sm:pr-0"
                  >
                    <a
                      href="#"
                      class="text-indigo-400 hover:text-indigo-300"
                      @click="editCall(projectsData, index)"
                      >Edit</a
                    >
                  </td>
                  <td
                    class="relative whitespace-nowrap py-4 pl-3 pr-4 text-right text-sm font-medium sm:pr-0"
                  >
                    <a
                      href="#"
                      class="text-indigo-400 hover:text-indigo-300"
                      @click="deleteCall(projectsData, index)"
                      >Delete</a
                    >
                  </td>
                </tr>
              </tbody>
            </table>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { defineEmits, defineProps } from "vue";

const emit = defineEmits(["openProjectSideBar", "editCall", "deleteCall"]);

const props = defineProps({
  projectsGetData: {
    type: Object,
  },
});

//Sending emit for opening sidebar
const addProjects = () => {
  emit("openProjectSideBar");
};

//sending emit for edit
const editCall = (projectsData: any, index: any) => {
  emit("editCall", projectsData, index);
};

//sending emit for delete
const deleteCall = (projectsData: any, index: any) => {
  emit("deleteCall", projectsData, index);
};
</script>
