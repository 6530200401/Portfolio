<template>
    <div class="card">
        <div class="card-body">
            <h5 class="text-primary">แก้ไขข้อมูลนิสิต</h5>
            <form @submit.prevent="handleSubmit()">
                <div class="row">
                    <div class="col-lg-12 col-md-12 col-sm-12 mt-2">
                        <label for="courseId" class="form-label">รหัสวิชา</label>
                        <input type="text" id="courseId" class="form-control" v-model.trim="in_course.id" />
                    </div>
                    <div class="col-lg-6 col-md-6 col-sm-6 mt-2">
                        <label for="courseNameTH" class="form-label">ชื่อวิชาภาษาไทย</label>
                        <input type="text" id="courseNameTH" class="form-control" v-model.trim="in_course.courseNameTH" />
                    </div>
                    <div class="col-lg-6 col-md-6 col-sm-6 mt-2">
                        <label for="courseNameEng" class="form-label">ชื่อวิชาภาษาอังกฤษ</label>
                        <input type="text" id="courseNameEng" class="form-control" v-model.trim="in_course.courseNameEng" />
                    </div>
                    <div class="col-lg-2 col-md-3 col-sm-4 mt-2">
                        <label for="credit" class="form-label">หน่วยกิต</label>
                        <input type="number" id="credit" class="form-control" v-model.trim="in_course.credit" />
                    </div>
                    <div class="col-lg-2 col-md-3 col-sm-4 mt-2">
                        <label for="grade" class="form-label">เกรด</label>
                        <input type="text" id="grade" class="form-control" v-model.trim="in_course.grade" />
                    </div>
                    <div class="col-lg-2 col-md-3 col-sm-4 mt-2">
                        <label for="studyYear" class="form-label">ปีการศึกษา</label>
                        <input type="number" id="studyYear" class="form-control" v-model.trim="in_course.studyYear" />
                    </div>
                    <div class="col-lg-2 col-md-3 col-sm-4 mt-2">
                        <label for="" class="form-label">ภาค</label>
                        <div class="form-check">
                            <input class="form-check-input" type="radio" id="semester" value="ภาคต้น" v-model="in_course.semester" />
                            <label class="form-check-label" for="semester">ภาคต้น</label>
                        </div>
                        <div class="form-check">
                            <input class="form-check-input" type="radio" id="semester" value="ภาคปลาย" v-model="in_course.semester" />
                            <label class="form-check-label" for="semester">ภาคปลาย</label>
                        </div>
                    </div>
                    <div class="col mx-5 my-5">
                        <button type="submit" class="btn btn-primary mx-3">
                            บันทึก
                        </button>
                        <button type="submit" class="btn btn-outline-info" @click="editData()">
                            Refresh
                        </button>
                    </div>
                </div>

            </form>

        </div>
    </div>
    <div class="alert alert-success mt-2" v-show="editSuccess">
        แก้ไขรายวิชา {{ in_course.id }}  {{ in_course.courseNameTH }} สำเร็จ
    </div>
    <div class="alert alert-success mt-2" v-show="editError">
        {{ errMessage }}
    </div>
</template>

<script>
export default {
    name:'CourseEdit',
    props:['ID'],
    data(){
        return{
            in_course:[],
            editSuccess:false,
            editError: false,
            errMessage:''
        }
    },
    mounted() {
    fetch('http://localhost:3000/students/' + this.ID)
        .then(res => res.json())
        .then(data => this.in_course = data)
        .catch(err => console.log(err.message))
},
    methods:{
        handleSubmit() {
    //สร้าง Object เพื่อเตรียมส่งข้อมูล - ค่า properties ที่ v-model กับ form ไว้
    let courses = {
        id: this.in_course.id,
        courseNameTH: this.in_course.courseNameTH,
        courseNameEng: this.in_course.courseNameEng,
        credit: this.in_course.credit,
        grade: this.in_course.grade,
        studyYear: this.in_course.studyYear,
        semester: this.in_course.semester,
        isShow: this.in_course.isShow
    }
    //กำหนดการติดต่อกับ endpoint ระบุ Method POST
    fetch('http://localhost:3000/students/' + this.ID, {
        method: 'PATCH',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify(courses)
    })
        .then(() => {
            this.editSuccess = true
        })
        .catch((err) => {
            this.editError = true
            this.editMessage = err
        })
    },
    editData(){
        this.$emit('edit')
    }

    }
}
</script>

<style>

</style>