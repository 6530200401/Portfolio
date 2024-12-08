<template>
  <nav class="navbar navbar-expand-lg navbar-light bg-dark sticky-top">
    <div class="container-fluid">
      <a
        class="navbar-brand d-flex align-items-center mb-3 mb-md-0 me-md-auto link-body-emphasis text-decoration-none"
        href="#"
      >
        <img
          src="./assets/secret_zerotwo.jpg"
          alt="Avatar Logo"
          style="width: 40px"
          class="rounded-pill"
        />
      </a>
      <div class="collapse navbar-collapse" id="navbarContent">
        <ul class="navbar-nav me-auto mb-2 mb-lg-0">
          <li class="nav-item">
            <a class="nav-link active" href="#"
              ><span class="fs-4 text-white">MY PORTFOLIO</span></a
            >
          </li>
        </ul>
        <ul class="nav nav-pills">
          <li class="nav-item">
            <a href="#" class="nav-link active text-white" aria-current="page"
              >Home</a
            >
          </li>
          <li class="nav-item">
            <a href="#person" class="nav-link text-white">About Me</a>
          </li>
          <li class="nav-item">
            <a href="#hobbie" class="nav-link text-white">Hobbie</a>
          </li>

          <li class="nav-item">
            <a href="#sub" class="nav-link text-white">Course Info</a>
          </li>
        </ul>
      </div>
    </div>
  </nav>
  <div class="bg-image text-black p-5" id="picture">
    <div>
      <h1 class="text-white text-center">
        สวัสดีครับ , ยินดีต้อนรับสู่ WEBSITE ของผม
      </h1>
      <h3 class="text-white text-center my-4">
        นี่คือ WEBSITE PORTFOLIO ที่รวมประวัติ งานอดิเรก และรายวิชาต่างๆ
      </h3>
      <h3 class="text-white text-center">
        มีทั้งชื่อวิชา เกรด ภาคการศึกษา เป็นต้น
      </h3>
    </div>
  </div>

  <div class="bg-black">
    <div class="container text-center mb-2">
      <div class="row">
        <div class="col py-5">
          <h1 class="text-white mb-4 display-3">คติประจำใจ</h1>
          <img src=".\assets\stone.jpg" alt="" class="img-thumbnail" />
        </div>
        <div class="col py-5">
          <img
            src=".\assets\Nisitpic.jpg"
            alt=""
            class="img-thumbnail"
            id="nisit"
          />
          <div id="person"></div>
        </div>
      </div>
    </div>
  </div>

  <div class="container-fluid bg-dark mb-4">
    <div class="row">
      <div class="col text-center text-white py-5">
        <h2 class="display-1 py-3">ประวัติ<br />About Me</h2>
      </div>
      <div class="col text-white py-5">
        <h2>ชื่อ : รัฐกิจ คชรินทร์</h2>
        <h2>อายุ : 21</h2>
        <h2>
          กำลังศึกษาปริญญาตรีที่ :<br />มหาวิทยาลัยเกษตรศาสตร์ วิทยาเขตศรีราชา
        </h2>
        <h2>คณะ : วิทยาศาสตร์</h2>
        <h2>สาขา : วิทยาการคอมพิวเตอร์</h2>
        <div id="hobbie"></div>
      </div>
    </div>
  </div>
  <div class="container text-center">
    <h2 class="display-1 mb-4">งานอดิเรก</h2>
    <div class="row">
      <div class="col">
        <h2>เล่นเกม</h2>
        <img
          src="./assets/play.jpg"
          alt=""
          class="img-thumbnail"
          width="400"
          height="400"
        />
      </div>
      <div class="col">
        <h2>นอน</h2>
        <img
          src="./assets/sleepTime.jpg"
          alt=""
          class="img-thumbnail"
          width="400"
          height="400"
        />
      </div>
      <div class="col">
        <h2>ฟังเพลง</h2>
        <img
          src="./assets/music.jpg"
          alt=""
          class="img-thumbnail"
          width="400"
          height="400"
        />
      </div>
    </div>
  </div>
  <div class="container-fluid bg-dark text-white mt-4">
    <h2 id="sub" class="display-1 text-center mb-5 pt-5">
      ข้อมูลรายวิชาที่ศึกษา
    </h2>
    <div class="row">
      <div class="col-6 d-flex justify-content-center pb-5">
        <div class="card" style="width: 400px">
          <img class="card-img-top" src="./assets/open.jpg" alt="Card image" />
          <div class="card-body d-flex flex-column">
            <h4 class="card-title">ดูรายวิชา</h4>
            <p class="card-text">
              แสดงแต่ละรายวิชาที่เรียนและเมื่อกดดูแต่ละวิชาก็จะมีรายละเอียดขึ้น
            </p>

            <a
              href="#subject"
              class="mt-auto btn btn-primary"
              @click="toggleShow()"
              >แสดงรายวิชา</a
            >
          </div>
        </div>
      </div>
      <div class="col-6 d-flex justify-content-center pb-5">
        <div class="card" style="width: 400px">
          <img class="card-img-top" src="./assets/write.jpg" alt="Card image" />
          <div class="card-body d-flex flex-column">
            <h4 class="card-title">เพิ่มรายวิชา</h4>
            <p class="card-text">เพิ่มรายวิชาที่ต้องการ</p>

            <a
              href="#subjectAdd"
              class="mt-auto btn btn-danger"
              @click="toggleAdd()"
              >เพิ่มรายวิชา</a
            >
          </div>
        </div>
      </div>
      <div class="col">
        <div class="m-5" v-if="showList">
          <CourseList id="subject" />
        </div>
        <div class="m-5" v-if="showAddTable">
          <CourseAdd id="subjectAdd" />
        </div>
      </div>
    </div>
  </div>

  <div class="m-2" v-if="showEdit">
    <CourseEdit />
  </div>
</template>

<script>
import CourseList from "./components/CourseList.vue";
import CourseAdd from "./components/CourseAdd.vue";

export default {
  name: "App",
  components: {
    CourseList,
    CourseAdd,
  },
  data() {
    return {
      showList: false,
      showAddTable: false,
      showEdit: false,
    };
  },
  methods: {
    toggleShow() {
      this.showList = !this.showList;
      this.showAddTable = false;
    },
    toggleAdd() {
      this.showAddTable = !this.showAddTable;
      this.showList = false;
    },
    toggleEdit() {
      this.showEdit = !this.showEdit;
    },
  },
};
</script>

<style>
</style>