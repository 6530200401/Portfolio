<template>
  <div class="card">
    <div class="card-body">
      <div class="card-title">รหัสวิชา : {{ students.id }}</div>
      <div class="card-title">ชื่อวิชา : {{ students.courseNameTH }}</div>
      <div class="card-title">หน่วยกิต : {{ students.credit }}</div>
      <div class="card-title">เกรด : {{ students.grade }}</div>
      <div class="card-title">ปีการศึกษา : {{ students.studyYear }}</div>
      <div class="card-title">ภาค : {{ students.semester }}</div>
    </div>
  </div>
  <div class="m-3">
    <button class="btn btn-warning mx-3 " @click="toggleEdit()">แก้ไขข้อมูล</button>
    <button class="btn btn-danger " @click="delDetail(courseID)">ลบรายวิชา</button>
  </div>
  
  <div class="m-2" v-if="showEdit">
      <CourseEdit :ID=numId @edit="editStatus" @delete="reload" />
      
    </div>
</template>

<script>
import CourseEdit from './CourseEdit.vue'
export default {
    name:'CourseDetail',
    props:['courseID'],
    components:{
      CourseEdit
    },
    data(){
      return{
        students:[],
        showEdit:false,
        numId:this.courseID
      }
    },
    mounted(){
      fetch('http://localhost:3000/students/' + this.courseID)
      .then(res=>res.json())
      .then(data=>this.students=data)
      .catch(err=>console.log(err.message))
    },
    methods:{
      delDetail(theID){
        fetch('http://localhost:3000/students/' + theID,{
            method:'DELETE'
        })
        .then(this.$emit('delete'))
        .catch()
      },
      toggleEdit(){
        this.showEdit=!this.showEdit
      },
      editStatus(){
        this.$emit('edit')
      }
    }
}
</script>

<style>

</style>