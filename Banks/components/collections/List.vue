<template>
  <div class="px-4 sm:px-6 lg:px-8 p-5">
    <div class="sm:flex sm:items-center">
      <div class="sm:flex-auto">
        <h1 class="text-base font-semibold leading-6 text-gray-900">Exam</h1>
        <p class="mt-2 text-sm text-gray-700">
          An examination or test is an educational assessment intended to
          measure a test-taker's knowledge, skill, aptitude, physical fitness,
          or classification in many other topics.
        </p>
      </div>
      <div class="mt-4 sm:ml-16 sm:mt-0 sm:flex-none">
        <button
          @click="addQuestion"
          type="button"
          class="block rounded-md bg-indigo-600 px-3 py-2 text-center text-sm font-semibold text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600"
        >
          Add Question
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
                  Category<Input:radio></Input:radio>
                </th>
                <th
                  scope="col"
                  class="px-4 py-3.5 text-center text-sm font-semibold text-gray-900"
                >
                  Skill
                </th>
                <th
                  scope="col"
                  class="px-4 py-3.5 text-center text-sm font-semibold text-gray-900"
                >
                  Question Type
                </th>
                <th
                  scope="col"
                  class="py-3.5 pl-4 pr-4 text-center text-sm font-semibold text-gray-900 sm:pr-0"
                >
                  Question
                </th>
                <th
                  scope="col"
                  class="px-4 py-3.5 text-center text-sm font-semibold text-gray-900"
                >
                  Answer Type
                </th>
                <th
                  scope="col"
                  class="py-3.5 pl-4 pr-4 text-center text-sm font-semibold text-gray-900 sm:pr-0"
                >
                  Answer Hint
                </th>
              </tr>
            </thead>
            <tbody class="divide-y divide-gray-200 bg-white">
              <!-- Here I have used data._rawValue for getting the GET Call data  -->
              <tr
                v-for="(examData, index) in getBanksData"
                :key="index"
                class="divide-x divide-gray-200"
              >
                <td
                  class="whitespace-nowrap py-4 text-center pl-4 pr-4 text-sm font-medium text-gray-900 sm:pl-0"
                >
                  {{ examData.category }}
                </td>
                <td
                  class="whitespace-nowrap text-center p-4 text-sm text-gray-500"
                >
                  {{ examData.skill }}
                </td>
                <td
                  class="whitespace-nowrap p-4 text-center text-sm text-gray-500"
                >
                  {{ examData.question_type }}
                </td>
                <td
                  class="whitespace-nowrap py-4 pl-4 text-center pr-4 text-sm text-gray-500 sm:pr-0"
                >
                  {{ examData.question }}
                </td>
                <td
                  class="whitespace-nowrap py-4 pl-4 text-center pr-4 text-sm text-gray-500 sm:pr-0"
                >
                  {{ examData.answer_type }}
                </td>
                <td
                  class="whitespace-nowrap py-4 pl-4 text-center pr-4 text-sm text-gray-500 sm:pr-0"
                >
                  {{ examData.answer_hint }}
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
  getBanksData: {
    type: Array,
  },
});

//Declaring Emits
const emit = defineEmits(["createExamModalPopup"]);
const addQuestion = () => {
  emit("createExamModalPopup");
};
</script>
