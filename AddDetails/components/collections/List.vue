<template>
  <button @click="addEmployeeDetails">Add Details</button>
  <ul
    role="list"
    class="grid grid-cols-1 gap-6 sm:grid-cols-2 lg:grid-cols-3 p-5 mt-[100px] bg-black"
  >
    <li
      v-for="(person, index) in employeeDetails"
      :key="index"
      class="col-span-1 divide-y divide-gray-200 rounded-lg bg-white shadow"
    >
      <div class="flex w-full items-center justify-between space-x-6 p-6">
        <div class="flex-1 truncate">
          <div class="flex items-center space-x-3">
            <h3 class="truncate text-sm font-medium text-gray-900">
              Name : {{ person.name }}
            </h3>
            <span
              class="inline-block flex-shrink-0 rounded-full bg-green-100 px-2 py-0.5 text-xs font-medium text-green-800"
              >Age : {{ person.age }}</span
            >
          </div>
          <p class="mt-1 truncate text-sm text-gray-500">
            Gender : {{ person.gender }}
          </p>
          <p class="mt-1 truncate text-sm text-gray-500">
            DOB : {{ person.dob }}
          </p>
        </div>
        <img
          class="h-10 w-10 flex-shrink-0 rounded-full bg-gray-300"
          src="https://creazilla-store.fra1.digitaloceanspaces.com/cliparts/7803/girl-taking-a-test-clipart-xl.png"
          alt=""
        />
      </div>
      <div>
        <div class="-mt-px flex divide-x divide-gray-200">
          <div class="flex w-0 flex-1">
            <a
              :href="`mailto:${person.dob}`"
              class="relative -mr-px inline-flex w-0 flex-1 items-center justify-center gap-x-3 rounded-bl-lg border border-transparent py-4 text-sm font-semibold text-gray-900"
            >
            </a>
          </div>
        </div>
      </div>
      <button @click="editEmployee(person, index)">Edit</button>
      <br />
      <button @click="open = true">Delete</button>
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
                  <div>
                    <div
                      class="mx-auto flex h-12 w-12 items-center justify-center rounded-full bg-green-100"
                    >
                      <CheckIcon
                        class="h-6 w-6 text-green-600"
                        aria-hidden="true"
                      />
                    </div>
                    <div class="mt-3 text-center sm:mt-5">
                      <DialogTitle
                        as="h3"
                        class="text-base font-semibold leading-6 text-gray-900"
                        >Are you sure want to delete</DialogTitle
                      >
                      <div class="mt-2">
                        <p class="text-sm text-gray-500">
                          This action shall permanently remove this message.
                          This cannot be undone!
                        </p>
                      </div>
                    </div>
                  </div>
                  <div
                    class="mt-5 sm:mt-6 sm:grid sm:grid-flow-row-dense sm:grid-cols-2 sm:gap-3"
                  >
                    <button
                      type="button"
                      class="inline-flex w-full justify-center rounded-md bg-red-600 px-3 py-2 text-sm font-semibold text-white shadow-sm hover:bg-red-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600 sm:col-start-2"
                      @click="deleteEmployee(person, index)"
                    >
                      Delete
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
    </li>
  </ul>
</template>

<script setup lang="ts">
import { EnvelopeIcon, PhoneIcon } from "@heroicons/vue/20/solid";
import { Vue2 } from "nuxt/dist/app/compat/vue-demi";
import { ref } from "vue";
const open = ref(true);

const props = defineProps({
  employeeDetails: {
    type: Array,
  },
});
// Declaring Emits
const emit = defineEmits([
  "addEmployeeDetails",
  "editEmployee",
  "deleteEmployee",
]);

const addEmployeeDetails = () => {
  emit("addEmployeeDetails");
};

const editEmployee = (person: any, index: any) => {
  emit("editEmployee", person, index);
};
const deleteEmployee = (person: any, index: any) => {
  emit("deleteEmployee", person, index);
};
</script>
