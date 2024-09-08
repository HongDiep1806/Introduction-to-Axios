<template>
  <CourseItem v-for="course in courses" :key="course.id" :fetchData="fetchData" :courseID="course.id"
    :coursename="course.name" :teacherID="course.teacherID">
  </CourseItem>


</template>
<script setup lang="ts">
import CourseItem from './CourseItem.vue';
import type { Course } from '../types/Course';
import UpdateCourseModal from './UpdateCourseModal.vue';

const props = withDefaults(
  defineProps<{

    courses: Course[],
    fetchData: () => void
  }>(),
  {
    courses: () => [],

  },
)

// const props = defineProps({
//   courses: Course[],
// })
</script>