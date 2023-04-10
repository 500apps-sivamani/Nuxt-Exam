<template>
  <div class="px-4 sm:px-6 lg:px-8">
    <div class="sm:flex sm:items-center">
      <div class="sm:flex-auto">
        <h1 class="text-base font-semibold leading-6 text-gray-900">
          Builders
        </h1>
        <p class="mt-2 text-sm text-gray-700">
          A list of all the Builders in your account including their name,
          email.
        </p>
      </div>
      <div class="mt-4 sm:ml-16 sm:mt-0 sm:flex-none">
        <button
          @click="addBuilder"
          type="button"
          class="block rounded-md bg-indigo-600 px-3 py-2 text-center text-sm font-semibold text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600"
        >
          Add Builder
        </button>
      </div>
    </div>
    <div class="mt-8 flow-root">
      <div class="-mx-4 -my-2 sm:-mx-6 lg:-mx-8">
        <div class="inline-block min-w-full py-2 align-middle">
          <table class="min-w-full border-separate border-spacing-0">
            <thead>
              <tr>
                <th
                  scope="col"
                  class="sticky top-0 z-10 border-b border-gray-300 bg-white bg-opacity-75 py-3.5 pl-4 pr-3 text-center text-sm font-semibold text-gray-900 backdrop-blur backdrop-filter sm:pl-6 lg:pl-8"
                >
                  Name
                </th>
                <th
                  scope="col"
                  class="sticky top-0 z-10 hidden border-b border-gray-300 bg-white bg-opacity-75 px-3 py-3.5 text-center text-sm font-semibold text-gray-900 backdrop-blur backdrop-filter sm:table-cell"
                >
                  Email
                </th>
                <th
                  scope="col"
                  class="sticky top-0 z-10 hidden border-b border-gray-300 bg-white bg-opacity-75 px-3 py-3.5 text-center text-sm font-semibold text-gray-900 backdrop-blur backdrop-filter lg:table-cell"
                >
                  Phone Number
                </th>
                <th
                  scope="col"
                  class="sticky top-0 z-10 border-b border-gray-300 bg-white bg-opacity-75 px-3 py-3.5 text-center text-sm font-semibold text-gray-900 backdrop-blur backdrop-filter"
                >
                  Established Year
                </th>
                <th
                  scope="col"
                  class="sticky top-0 z-10 border-b border-gray-300 bg-white bg-opacity-75 px-3 py-3.5 text-center text-sm font-semibold text-gray-900 backdrop-blur backdrop-filter"
                >
                  Tag Line
                </th>
                <th
                  scope="col"
                  class="sticky top-0 z-10 border-b border-gray-300 bg-white bg-opacity-75 py-3.5 pl-3 backdrop-blur backdrop-filter sm:pr-6 lg:pr-8"
                >
                  <span class="sr-only">Edit</span>
                </th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="(person, index) in getBuilders" :key="index">
                <td
                  :class="[
                    index !== getBuilders.length - 1
                      ? 'border-b border-gray-200'
                      : '',
                    'whitespace-nowrap py-4 pl-4 pr-3 text-center text-sm font-medium text-gray-900 sm:pl-6 lg:pl-8',
                  ]"
                >
                  {{ person.name }}
                </td>
                <td
                  :class="[
                    index !== getBuilders.length - 1
                      ? 'border-b border-gray-200'
                      : '',
                    'whitespace-nowrap hidden px-3 text-center py-4 text-sm text-gray-500 sm:table-cell',
                  ]"
                >
                  {{ person.email }}
                </td>
                <td
                  :class="[
                    index !== getBuilders.length - 1
                      ? 'border-b border-gray-200'
                      : '',
                    'whitespace-nowrap hidden text-center px-3 py-4 text-sm text-gray-500 lg:table-cell',
                  ]"
                >
                  {{ person.phone_number }}
                </td>
                <td
                  :class="[
                    index !== getBuilders.length - 1
                      ? 'border-b border-gray-200'
                      : '',
                    'whitespace-nowrap text-center px-3 py-4 text-sm text-gray-500',
                  ]"
                >
                  {{ person.established_year }}
                </td>
                <td
                  :class="[
                    index !== getBuilders.length - 1
                      ? 'border-b border-gray-200'
                      : '',
                    'whitespace-nowrap text-center px-3 py-4 text-sm text-gray-500',
                  ]"
                >
                  {{ person.tag_line }}
                </td>
                <td
                  :class="[
                    index !== getBuilders.length - 1
                      ? 'border-b border-gray-200'
                      : '',
                    'relative whitespace-nowrap py-4 pr-4 pl-3 text-right text-sm font-medium sm:pr-8 lg:pr-8',
                  ]"
                >
                  <a
                    @click="editCall(person, index)"
                    href="#"
                    class="text-indigo-600 hover:text-indigo-900"
                    >Edit</a
                  >
                </td>
                <td
                  :class="[
                    index !== getBuilders.length - 1
                      ? 'border-b border-gray-200'
                      : '',
                    'relative whitespace-nowrap py-4 pr-4 pl-3 text-right text-sm font-medium sm:pr-8 lg:pr-8',
                  ]"
                >
                  <a
                    @click="deleteCall(person, index)"
                    href="#"
                    class="text-indigo-600 hover:text-indigo-900"
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
</template>

<script setup lang="ts">
const people = [
  {
    name: "Lindsay Walton",
    title: "Front-end Developer",
    email: "lindsay.walton@example.com",
    role: "Member",
  },
  // More people...
];

//Declaring Props to pass the data from Main file to list files through props
const props = defineProps({
  getBuilders: {
    type: Array,
  },
});

//Declaring Emits to access the data from Main File
const emit = defineEmits(["addBuilderSidebar", "editCall", "deleteCall"]);

const addBuilder = () => {
  emit("addBuilderSidebar");
};

const editCall = (person: any, index: any) => {
  emit("editCall", person, index);
};

const deleteCall = (person: any, index: any) => {
  emit("deleteCall", person, index);
};
</script>
