<template>
  <div class="px-4 sm:px-6 lg:px-8 p-5">
    <div class="sm:flex sm:items-center">
      <div class="sm:flex-auto">
        <h1 class="text-base font-semibold leading-6 text-gray-900">Jobs</h1>
        <p class="mt-2 text-sm text-gray-700">
          A job posting is an official advertisement of job openings published
          for job seekers.
        </p>
      </div>
      <div class="mt-4 sm:ml-16 sm:mt-0 sm:flex-none">
        <button
          @click="createJob"
          type="button"
          class="block rounded-md bg-indigo-600 px-3 py-2 text-center text-sm font-semibold text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600"
        >
          Create Job
        </button>
      </div>
    </div>
    <div class="mt-8 flow-root">
      <div class="-mx-4 -my-2 overflow-x-auto sm:-mx-6 lg:-mx-8">
        <div class="inline-block min-w-full py-2 align-middle sm:px-6 lg:px-8">
          <table class="min-w-full divide-y divide-gray-300">
            <thead>
              <tr class="divide-x divide-gray-200">
                <th
                  scope="col"
                  class="py-3.5 pl-4 pr-4 text-center text-sm font-semibold text-gray-900 sm:pl-0"
                >
                  Job ID <Input:radio></Input:radio>
                </th>
                <th
                  scope="col"
                  class="px-4 py-3.5 text-center text-sm font-semibold text-gray-900"
                >
                  Status
                </th>
                <th
                  scope="col"
                  class="px-4 py-3.5 text-center text-sm font-semibold text-gray-900"
                >
                  Resume URL
                </th>
                <th
                  scope="col"
                  class="py-3.5 pl-4 pr-4 text-center text-sm font-semibold text-gray-900 sm:pr-0"
                >
                  CoverLetter URL
                </th>
              </tr>
            </thead>
            <tbody class="divide-y divide-gray-200 bg-white">
              <!-- Here I have used data._rawValue for getting the GET Call data  -->
              <tr
                v-for="(jobPosting, index) in $props.getApplicationData"
                :key="index"
                class="divide-x divide-gray-200"
              >
                <td
                  class="whitespace-nowrap py-4 text-center pl-4 pr-4 text-sm font-medium text-gray-900 sm:pl-0"
                >
                  {{ jobPosting.job_posting_id }}
                </td>
                <td
                  class="whitespace-nowrap text-center p-4 text-sm text-gray-500"
                >
                  {{ jobPosting.status }}
                </td>
                <td
                  class="whitespace-nowrap p-4 text-center text-sm text-gray-500"
                >
                  {{ jobPosting.resume_url }}
                </td>
                <td
                  class="whitespace-nowrap py-4 pl-4 text-center pr-4 text-sm text-gray-500 sm:pr-0"
                >
                  {{ jobPosting.cover_letter }}
                </td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { defineProps, defineEmits } from "vue";

//Delcaring Props
const props = defineProps({
  getApplicationData: {
    type: Array,
  },
});

//Declaring Emits
const emit = defineEmits(["createJobModalPopup"]);
const createJob = () => {
  emit("createJobModalPopup");
};
</script>
