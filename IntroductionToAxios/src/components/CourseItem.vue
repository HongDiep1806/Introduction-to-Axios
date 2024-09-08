<template>
    <div class="container">
        <div class="left">
            <h4>Course Name: {{ props.coursename }}</h4>
            <p>{{ props.courseID }}</p>
            <p>{{ props.teacherID }}</p>
        </div>
        <div class="right">
            <button @click="deleteCourse">Delete</button>
            <button>Update</button>
        </div>
    </div>
</template>

<script setup lang="ts">
import axios from 'axios';

const deleteCourse = async () => {
    try {
        const trimmedId = props.courseID.trim();
        const response = await axios.delete('https://localhost:7117/api/Course/', {
            data: {
                id: trimmedId
            }
        });
        console.log(response.data);
        alert("Delete successfully");
        await props.fetchData();
    } catch (error) {
        console.error("There was an error deleting the data:", error);
    }
}
const props = defineProps<{
    courseID: string,
    coursename: string,
    teacherID: string,
    fetchData: () => void
}>()
</script>

<style scoped>
.container {
    width: 100%;
    display: flex;
    justify-content: space-between;
    align-items: center;
    border-top: 1px solid black;
    margin: 0;
    padding: 0;
}

.left {
    flex: 1;
    width: 100%;
    margin: 10px 10px;
}

.right {
    flex: 0;
    display: flex;
    gap: 10px;
    padding: 50px;
}

button {
    padding: 5px 10px;
    width: 100px;
    background-color: green;
    color: white;
    border-radius: 5px;
}

h4 {
    color: green;
}
</style>
