<script setup lang="ts">
import { ref } from 'vue';
import axios from 'axios';
import CourseItem from './components/CourseItem.vue';
import type { Course } from './types/Course';
import CourseTableItem from './components/CourseTableItem.vue';
import CreateCourse from './components/CreateCourse.vue';

const courses = ref<Course[]>([]);
const idUpdate = ref('');
const nameUpdate = ref('');
const teacherIDUpdate = ref('');
const fetchData = async () => {
  try {
    const response = await axios.get('https://localhost:7117/api/Course');
    courses.value = response.data;
  } catch (error) {
    console.error("There was an error fetching the data:", error);
  }
}
const updateCourse = async () => {
  try {
    const trimmedId = idUpdate.value.trim();
    const response = await axios.put('https://localhost:7117/api/Course/', {
      id: trimmedId,
      name: nameUpdate.value,
      teacherID: teacherIDUpdate.value

    });
    console.log(response.data);
    alert("Update successfully");
    await fetchData();
    idUpdate.value = '';
    nameUpdate.value = '';
    teacherIDUpdate.value = '';
  } catch (error) {
    console.error("There was an error deleting the data:", error);
  }
}
</script>

<template>
  <div class="container">
    <div class="left-side">
      <h1>Test Axios</h1>
      <h2>Get All Course</h2>
      <button @click="fetchData"
        style="margin-top: 10px;padding: 5px 10px;border-radius: 5px; background-color: green; color: white">Get
        All</button>
      <br>
      <CreateCourse :fetch-data="fetchData">
      </CreateCourse>
    </div>
    <div class="right-side" v-if="courses.length">
      <CourseTableItem :fetch-data="fetchData" :courses="courses">
      </CourseTableItem>
    </div>

  </div>





</template>

<style scoped>
.container {
  display: flex;
  justify-content: space-between;
  padding: 20px;
}

.left-side,
.righ-side {
  flex: 1;
  padding: 10px;
}
</style>
