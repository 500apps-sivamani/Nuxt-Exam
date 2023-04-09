<template>
  <TransitionRoot as="template" :show="open">
    <Dialog as="div" class="relative z-10" @close="open = false">
      <TransitionChild
        as="template"
        enter="ease-out duration-300"
        enter-from="opacity-0"
        enter-to="opacity-100"
        leave="ease-in duration-200"
        leave-from="opacity-100"
        leave-to="opacity-0"
      >
        <div
          class="fixed inset-0 bg-gray-500 bg-opacity-75 transition-opacity"
        />
      </TransitionChild>

      <div class="fixed inset-0 z-10 overflow-y-auto">
        <div
          class="flex min-h-full items-end justify-center p-4 text-center sm:items-center sm:p-0"
        >
          <TransitionChild
            as="template"
            enter="ease-out duration-300"
            enter-from="opacity-0 translate-y-4 sm:translate-y-0 sm:scale-95"
            enter-to="opacity-100 translate-y-0 sm:scale-100"
            leave="ease-in duration-200"
            leave-from="opacity-100 translate-y-0 sm:scale-100"
            leave-to="opacity-0 translate-y-4 sm:translate-y-0 sm:scale-95"
          >
            <DialogPanel
              class="relative transform overflow-hidden rounded-lg bg-white px-4 pb-4 pt-5 text-left shadow-xl transition-all sm:my-8 sm:w-full sm:max-w-lg sm:p-6"
            >
              <!-- your content goes here -->
              <div class="mt-6 py-6">
                <label />Category
                <input
                  v-model="bankCateogory"
                  type="text"
                  class="block mb-3 px-3 rounded-md border-0 py-2 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-300 sm:text-sm sm:leading-6 w-[100%]"
                />
                <label />Skill
                <input
                  v-model="bankSkill"
                  type="text"
                  class="block mb-3 px-3 rounded-md border-0 py-2 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-300 sm:text-sm sm:leading-6 w-[100%]"
                />
                <label for="test-type">Question Type</label>
                <select
                  v-model="bankQuestionType"
                  class="block mb-3 px-3 rounded-md border-0 py-3 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-300 sm:text-sm sm:leading-6 w-[100%]"
                >
                  <option selected value="">Please select Type</option>
                  <option value="text">text</option>
                  <option value="audio">audio</option>
                  <option value="video">video</option>
                </select>

                <label />Questions
                <input
                  v-model="bankQuestion"
                  type="text"
                  class="p-4 mb-3 block w-full rounded-md border-0 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-300 sm:py-1.5 sm:text-sm sm:leading-6"
                />
                <label for="test-type">Answer Type</label>
                <select
                  v-model="bankAnswerType"
                  class="block mb-3 px-3 rounded-md border-0 py-3 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-300 sm:text-sm sm:leading-6 w-[100%]"
                >
                  <option selected value="">Please select Type</option>
                  <option value="short">short</option>
                  <option value="text">text</option>
                  <option value="numeric">numeric</option>
                  <option value="mcq">mcq</option>
                  <option value="boolean">boolean</option>
                </select>
                <label for="test-type">Difficulty Level</label>
                <select
                  v-model="bankDifficulty"
                  class="block mb-3 px-3 rounded-md border-0 py-3 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-300 sm:text-sm sm:leading-6 w-[100%]"
                >
                  <option selected value="">Please select Type</option>
                  <option value="easy">easy</option>
                  <option value="medium">medium</option>
                  <option value="hard">hard</option>
                </select>

                <label />Answer Hint
                <input
                  v-model="bankAnswerHint"
                  type="text"
                  class="block mb-3 px-3 rounded-md border-0 py-2 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-300 sm:text-sm sm:leading-6 w-[100%]"
                />
              </div>
              <div
                class="mt-5 sm:mt-6 sm:grid sm:grid-flow-row-dense sm:grid-cols-2 sm:gap-3"
              >
                <button
                  type="button"
                  class="inline-flex w-full justify-center rounded-md bg-indigo-600 px-3 py-2 text-sm font-semibold text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600 sm:col-start-2"
                  @click="bankSubmitForm()"
                >
                  Submit
                </button>
                <button
                  type="button"
                  class="mt-3 inline-flex w-full justify-center rounded-md bg-white px-3 py-2 text-sm font-semibold text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 hover:bg-gray-50 sm:col-start-1 sm:mt-0"
                  @click="open = false"
                  ref="cancelButtonRef"
                >
                  Cancel
                </button>
              </div>
            </DialogPanel>
          </TransitionChild>
        </div>
      </div>
    </Dialog>
  </TransitionRoot>
</template>

<script setup>
import { ref, defineEmits, defineProps } from "vue";
import {
  Dialog,
  DialogPanel,
  DialogTitle,
  TransitionChild,
  TransitionRoot,
} from "@headlessui/vue";
import { CheckIcon } from "@heroicons/vue/24/outline";

const open = ref(true);

let bankCateogory = ref("");
let bankSkill = ref("");
let bankQuestionType = ref("");
let bankQuestion = ref("");
let bankAnswerType = ref("");
let bankDifficulty = ref("");
let bankAnswerHint = ref("");

const emit = defineEmits(["banksBody"]);

const bankSubmitForm = async () => {
  let body = [
    {
      category: bankCateogory.value,
      skill: bankSkill.value,
      question_type: bankQuestionType.value,
      question: bankQuestion.value,
      answer_type: bankAnswerType.value,
      answer: "string",
      answer_rules: {},
      sub_skill: "string",
      question_url: "string",
      answer_hint: bankAnswerHint.value,
      explanation: "string",
      difficulty_level: bankDifficulty.value,
      marks: 0,
      question_rules: {},
      mark_rules: {},
      id: 0,
    },
  ];
  emit("banksBody", body);
};
</script>
