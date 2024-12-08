<template>
  <ul class="list-group">
    <li v-for="(course, CID) in students" :key="CID" class="list-group-item">
      <a href="#a" @click="setShow(course)">
        {{ course.id }} {{ course.courseNameTH }}
      </a>
      <div v-if="course.isShow">
        <CourseDetail :courseID="course.id" @edit="reload" @delete="reload" />
      </div>
    </li>
  </ul>
</template>
<script>
import CourseDetail from "./CourseDetail.vue";

export default {
  name: "CouseList",
  components: {
    CourseDetail,
  },
  data() {
    return {
      students: [],
    };
  },
  mounted() {
    fetch("http://localhost:3000/students")
      .then((res) => res.json())
      .then((data) => (this.students = data))
      .catch((err) => console.log(err.message));
  },
  methods: {
    setShow(id) {
      id.isShow = !id.isShow;
    },
    reload() {
      this.$parent.showList = !this.$parent.showList;
    },
  },
};
</script>

<style></style>