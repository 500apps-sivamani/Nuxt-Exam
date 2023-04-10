<template>
  <CollectionsList
    :employeeDetails="employeeArray"
    @addEmployeeDetails="openAddEmployeeDetailsModal"
    @deleteEmployee="deleteEmployeeLocally"
    @editEmployee="editEmployeeLocally"
  />

  <div v-if="is_modal" :key="render">
    <CollectionsAdd @employeeForm="employeeForm" />
  </div>
  <div v-if="is_edit" :key="render">
    <CollectionsEdit :employeeDetails="employeeDetail" />
  </div>
</template>

<script setup lang="ts">
const is_modal = ref(false);
const render = ref(0);
const employeeArray = ref([]);
const is_edit = ref(false);
const employeeDetail = ref({});

const openAddEmployeeDetailsModal = () => {
  is_modal.value = true;
  render.value++;
};

onMounted(() => {
  const storedData = localStorage.getItem("formData");
  if (storedData) {
    employeeArray.value = JSON.parse(storedData);
  }
});

//Add employee Details Locally using Local Storage
const employeeForm = (data: any) => {
  employeeArray.value.push(data);
  localStorage.setItem("formData", JSON.stringify(employeeArray.value));
  is_modal.value = false;
};

//Edit Employee Locally
const editEmployeeLocally = (empDetail, index) => {
  console.log(empDetail, index);
  employeeDetail.value = empDetail;
  render.value++;
  is_edit.value = true;
};

//Delete Employee Permanently
const deleteEmployeeLocally = (index: number) => {
  employeeArray.value.splice(index, 1);
  localStorage.setItem("formData", JSON.stringify(employeeArray.value));
};
</script>
