<template>
    <div>
        <h2>Create new course</h2>
        <label for="nameC">Course Name</label>
        <br>
        <input v-model="courseName" id="nameC" type="text" placeholder="Enter new course name">
        <br>
        <label for="teacher">Teacher ID</label>
        <br>
        <input v-model="courseteacherID" id="teacher" type="text" placeholder="Enter teacher id">
        <br>
        <button @click="createNewCourse"
            style="margin-top: 10px;padding: 5px 10px;border-radius: 5px; background-color: green; color: white">
            Create
        </button>
    </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import axios from 'axios';

const props = defineProps<{
    fetchData: () => void;
}>();

const courseName = ref('');
const courseteacherID = ref('');

const createNewCourse = async () => {
    try {
        const response = await axios.post('https://localhost:7117/api/Course', {
            name: courseName.value,
            teacherID: courseteacherID.value
        });
        console.log(response.data);
        alert("Course created successfully");
        await props.fetchData();
        courseName.value = '';
        courseteacherID.value = '';
    } catch (error) {
        console.error("There was an error creating the course:", error);
    }
}
</script>

<style scoped></style>