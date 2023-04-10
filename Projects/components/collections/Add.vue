<template>
  <div>
    <TransitionRoot as="template" :show="open">
      <Dialog as="div" class="relative z-10" @close="open = false">
        <div class="fixed inset-0" />

        <div class="fixed inset-0 overflow-hidden">
          <div class="absolute inset-0 overflow-hidden">
            <div
              class="pointer-events-none fixed inset-y-0 right-0 flex max-w-full pl-10 sm:pl-16"
            >
              <TransitionChild
                as="template"
                enter="transform transition ease-in-out duration-500 sm:duration-700"
                enter-from="translate-x-full"
                enter-to="translate-x-0"
                leave="transform transition ease-in-out duration-500 sm:duration-700"
                leave-from="translate-x-0"
                leave-to="translate-x-full"
              >
                <DialogPanel class="pointer-events-auto w-screen max-w-2xl">
                  <div
                    class="flex h-full flex-col overflow-y-scroll bg-white py-6 shadow-xl"
                  >
                    <div class="px-4 sm:px-6">
                      <div class="items-start justify-between">
                        <DialogTitle
                          class="text-base font-semibold leading-6 text-white-900 mb-5"
                          >Add Candidates</DialogTitle
                        >
                        <hr />

                        <div class="mt-6 py-6">
                          <label />Name
                          <input
                            placeholder="(Please Enter Project Name Eg:RealEstate Ventures)"
                            v-model="projectName"
                            type="text"
                            class="block mb-3 px-3 rounded-md border-0 py-2 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-300 sm:text-sm sm:leading-6 w-[100%]"
                          />
                          <label for="test-type">Category</label>
                          <select
                            v-model="projectsCategory"
                            class="block mb-3 px-3 rounded-md border-0 py-3 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-300 sm:text-sm sm:leading-6 w-[100%]"
                          >
                            <option selected value="">
                              Please select Type
                            </option>
                            <option value="Residential">Residential</option>
                            <option value="Commercial">Commercial</option>
                          </select>

                          <label for="test-type">Sub Category</label>
                          <select
                            v-model="projectsSubCategory"
                            class="block mb-3 px-3 rounded-md border-0 py-3 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-300 sm:text-sm sm:leading-6 w-[100%]"
                          >
                            <option selected value="">
                              Please select Type
                            </option>
                            <option value="Apartment">Apartment</option>
                            <option value="Villa">Villa</option>
                            <option value="Plot">Plot</option>
                            <option value="Hybrid">Hybrid</option>
                            <option value="Office Space">Office Space</option>
                            <option value="Shop">Shop</option>
                          </select>
                          <label for="test-type">Status</label>
                          <select
                            v-model="projectStatus"
                            class="block mb-3 px-3 rounded-md border-0 py-3 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-300 sm:text-sm sm:leading-6 w-[100%]"
                          >
                            <option selected value="">
                              Please select Type
                            </option>
                            <option value="Fully Constructed">
                              Fully Constructed
                            </option>
                            <option value="Under Construction">
                              Under Construction
                            </option>
                            <option value="New Venture">New Venture</option>
                          </select>
                          <label for="test-type">Metric</label>
                          <select
                            v-model="projectMetric"
                            class="block mb-3 px-3 rounded-md border-0 py-3 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-300 sm:text-sm sm:leading-6 w-[100%]"
                          >
                            <option selected value="">
                              Please select Type
                            </option>
                            <option value="sq.ft">sq.ft</option>
                            <option value="sq.yards">sq.yards</option>
                            <option value="sq.m">sq.m</option>
                            <option value="acres">acres</option>
                            <option value="marla">marla</option>
                            <option value="cents">cents</option>
                            <option value="bigha">bigha</option>
                            <option value="kottah">kottah</option>
                            <option value="kanal">kanal</option>
                            <option value="grounds">grounds</option>
                            <option value="ares">ares</option>
                            <option value="biswa">biswa</option>
                            <option value="guntha">guntha</option>
                            <option value="aankadam">aankadam</option>
                            <option value="hectares">hectares</option>
                            <option value="rood">rood</option>
                            <option value="chataks">chataks</option>
                            <option value="perch">perch</option>
                          </select>

                          <label for="test-type">Approve Category</label>
                          <select
                            v-model="projectApproveCategory"
                            class="block mb-3 px-3 rounded-md border-0 py-3 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-300 sm:text-sm sm:leading-6 w-[100%]"
                          >
                            <option selected value="">
                              Please select Type
                            </option>
                            <option value="Under Review">Under Review</option>
                            <option value="Rejected">Rejected</option>
                            <option value="Active">Active</option>
                            <option value="Deleted">Deleted</option>
                            <option value="Expiring Soon">Expiring Soon</option>
                            <option value="Expired">Expired</option>
                            <option value="Inactive">Inactive</option>
                          </select>
                        </div>

                        <div class="ml-3 flex h-7 items-center">
                          <button
                            type="button"
                            class="rounded-md bg-white text-gray-400 hover:text-gray-500 focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:ring-offset-2"
                            @click="open = false"
                          >
                            <span class="sr-only">Close panel</span>
                          </button>
                        </div>
                      </div>
                    </div>
                    <div class="relative flex-1 px-2 sm:px-6">
                      <!-- Your content -->
                      <div class="bg-gray h-auto">
                        <div class="bg-gray-50 mx-auto px-4 py-3">
                          <div class="text-center mb-0 rounded-0">
                            <div class="flex justify-end mr-3 mt-4">
                              <button
                                @click="open = false"
                                type="button"
                                class="border rounded-md bg-white py-2 px-3 text-sm font-semibold text-gray-600 shadow-sm hover:bg-gray-50 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600 mr-3"
                              >
                                Cancel
                              </button>
                              <button
                                type="button"
                                class="rounded-md bg-indigo-600 py-2 px-4 text-sm font-semibold text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600"
                                @click="projectsSaveCall()"
                              >
                                Save
                              </button>
                            </div>
                          </div>
                        </div>
                      </div>
                    </div>
                  </div>
                </DialogPanel>
              </TransitionChild>
            </div>
          </div>
        </div>
      </Dialog>
    </TransitionRoot>
  </div>
</template>
<script setup lang="ts">
import { ref, defineEmits } from "vue";

import {
  Dialog,
  DialogPanel,
  DialogTitle,
  TransitionChild,
  TransitionRoot,
} from "@headlessui/vue";

//Declaring the V-model names
let projectName = ref("");
let projectsCategory = ref("");
let projectsSubCategory = ref("");
let projectStatus = ref("");
let projectMetric = ref("");
let projectApproveCategory = ref("");

const open = ref(true);

//Declaring the emits
const emit = defineEmits(["projectsBody"]);

//Sending body through the emit
const projectsSaveCall = async () => {
  let body = {
    name: projectName.value,
    listing_type_name: "dgdgd",
    category: projectsCategory.value,
    sub_category: projectsSubCategory.value,
    status: projectStatus.value,
    details: "stringfh",
    specifications: "sfsdfsdf",
    possession_date: "2023-04-09",
    age_of_the_project: "sfdsfsdf",
    logo_url: "sfdsdfsdf",
    total_project_area: 0,
    metric: projectMetric.value,
    default_image_url: "strsfding",
    visit_count: 0,
    rera_approved: true,
    approve_status: projectApproveCategory.value,
  };
  emit("projectsBody", body);
};
</script>
