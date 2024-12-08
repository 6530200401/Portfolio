<template>
         <div class="card">
        <div class="card-body">
            <form @submit.prevent="handleSubmit()">
                <div class="row">
                    <div class="col-lg-12 col-md-12 col-sm-12 mt-2">
                        <label for="courseId" class="form-label">รหัสวิชา</label>
                        <input type="text" id="courseId" class="form-control" v-model.trim="in_course.CID" required />
                    </div>
                    <div class="col-lg-6 col-md-6 col-sm-6 mt-2">
                        <label for="courseNameTH" class="form-label">ชื่อวิชาภาษาไทย</label>
                        <input type="text" id="courseNameTH" class="form-control" v-model.trim="in_course.courseNameTH" required />
                    </div>
                    <div class="col-lg-6 col-md-6 col-sm-6 mt-2">
                        <label for="courseNameEng" class="form-label">ชื่อวิชาภาษาอังกฤษ</label>
                        <input type="text" id="courseNameEng" class="form-control" v-model.trim="in_course.courseNameEng" required />
                    </div>
                    <div class="col-lg-2 col-md-3 col-sm-4 mt-2">
                        <label for="credit" class="form-label">หน่วยกิต</label>
                        <input type="number" id="credit" class="form-control" v-model.trim="in_course.credit" required />
                    </div>
                    <div class="col-lg-2 col-md-3 col-sm-4 mt-2">
                        <label for="grade" class="form-label">เกรด</label>
                        <input type="text" id="grade" class="form-control" v-model.trim="in_course.grade" required />
                    </div>
                    <div class="col-lg-2 col-md-3 col-sm-4 mt-2">
                        <label for="studyYear" class="form-label">ปีการศึกษา</label>
                        <input type="number" id="studyYear" class="form-control" v-model.trim="in_course.studyYear" required/>
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
                    <!-- <div class="col-lg-2 col-md-3 col-sm-4 mt-2">
                        <label for="stdYr" class="form-label">ชั้นปี</label>
                        <select id="stdYr" class="form-select" v-model="stds.yr">
                            <option value="1">ปี1</option>
                            <option value="2">ปี2</option>
                            <option value="3">ปี3</option>
                            <option value="4">ปี4</option>
                            <option value="5">เกินปี4</option>
                        </select>
                    </div> -->
                    <div class="col mx-5 my-5">
                        <button type="submit" class="btn btn-primary">
                            บันทึก
                        </button>
                    </div>
                </div>

            </form>

        </div>
    </div>
    <div class="alert alert-success mt-2" v-show="addSuccess">
        บันทึกรายวิชา {{ in_course.CID }}  {{ in_course.courseNameTH }}
    </div>
</template>

<script>
export default {
    name:'CourseAdd',
    data(){
        return {
            in_course:{
                CID:"",
                courseNameTH:"",
                courseNameEng:"",
                credit: "",
                grade: "",
                studyYear: 2567,
                semester: "ภาคต้น",
                isShow: false
            },
            addSuccess: false,
            addError:false,
            errMessage:""
        }
    },
    methods:{
        handleSubmit(){
            let courses = {
                id: this.in_course.CID,
                courseNameTH: this.in_course.courseNameTH,
                courseNameEng: this.in_course.courseNameEng,
                credit: this.in_course.credit,
                grade: this.in_course.grade,
                studyYear: this.in_course.studyYear,
                semester: this.in_course.semester,
                isShow: this.in_course.isShow
            }
            fetch('http://localhost:3000/students',{
                method:'POST',
                headers:{'Content-Type':'application/json'},
                body: JSON.stringify(courses)
            })
            .then(() => {
                this.addSuccess = true
            })
            .catch((err) => {
                this.addError = true
                this.errMessage = err
            })
        }
    }
}
</script>

<style>

</style>