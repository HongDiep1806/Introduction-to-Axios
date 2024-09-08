<template>
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
    <button @click="">Update</button>
</template>
<script>

</script>
<style></style>