<template>
    <div class="modal" v-if="courseID">
        <div class="modal-content">
            <span class="close-button" @click="closeModal">&times;</span>
            <h2>Update Course</h2>
            <label for="idUpdate">ID:</label>
            <input v-model="localCourseID" type="text" id="idUpdate" readonly>
            <br>
            <label for="nameUpdate">New course name:</label>
            <input v-model="localCourseName" type="text" id="nameUpdate" placeholder="Enter new course name">
            <br>
            <label for="teacherID">New teacher ID:</label>
            <input v-model="localCourseTeacherID" type="text" id="teacherID" placeholder="Enter teacher ID">
            <br>
            <button @click="updateCourse">Update</button>
        </div>
    </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import axios from 'axios';

const props = defineProps<{
    courseID: string,
    courseName: string,
    courseTeacherID: string
}>();

const emit = defineEmits(['close', 'updated']);

// Local reactive properties
const localCourseID = ref(props.courseID);
const localCourseName = ref(props.courseName);
const localCourseTeacherID = ref(props.courseTeacherID);

const closeModal = () => {
    emit('close');
};

const updateCourse = async () => {
    try {
        const response = await axios.put('https://localhost:7117/api/Course/', {
            id: localCourseID.value,
            name: localCourseName.value,
            teacherID: localCourseTeacherID.value
        });
        console.log(response.data);
        alert("Course updated successfully");
        emit('updated');
        closeModal();
    } catch (error) {
        console.error("Error updating course:", error);
    }
};
</script>

<style scoped>
.modal {
    /* Modal styling */
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.5);
    display: flex;
    justify-content: center;
    align-items: center;
}

.modal-content {
    background-color: white;
    padding: 20px;
    border-radius: 5px;
    width: 80%;
    max-width: 500px;
    position: relative;
}

.close-button {
    position: absolute;
    top: 10px;
    right: 10px;
    cursor: pointer;
    font-size: 24px;
}
</style>
