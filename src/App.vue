<template>
  <div>
    <nav class="navbar navbar-expand-lg navbar-light bg-white border-bottom fixed-top shadow-sm px-4" style="height: 60px;display:fixed;">
  <div class="container-fluid d-flex align-items-center justify-content-between">

    <!-- Brand -->
    <a class="navbar-brand d-flex align-items-center gap-2 fw-semibold text-dark" href="#">
      <div class="d-flex align-items-center justify-content-center rounded-2 bg-primary bg-opacity-10" style="width:34px;height:34px;">
        <svg width="18" height="18" viewBox="0 0 16 16" fill="none" xmlns="http://www.w3.org/2000/svg">
          <circle cx="8" cy="5" r="3" fill="#0d6efd"/>
          <path d="M2 13c0-3.314 2.686-5 6-5s6 1.686 6 5" stroke="#0d6efd" stroke-width="1.5" stroke-linecap="round"/>
        </svg>
      </div>
      Employee Management
    </a>
    <div class="d-flex align-items-center gap-2">
      <a href="#pstd" class="btn btn-sm d-flex align-items-center gap-2 px-3 text-secondary fw-medium nav-action" style="font-size:13px; border-radius:8px;">
        <svg width="14" height="14" viewBox="0 0 14 14" fill="none">
          <path d="M7 1v12M1 7h12" stroke="currentColor" stroke-width="1.6" stroke-linecap="round"/>
        </svg>
        Add
      </a>
      <a href="#vwd" class="btn btn-sm d-flex align-items-center gap-2 px-3 text-secondary fw-medium nav-action" style="font-size:13px; border-radius:8px;">
  <svg width="14" height="14" viewBox="0 0 14 14" fill="none">
    <path d="M1 4h12M1 7h12M1 10h8" stroke="currentColor" stroke-width="1.5" stroke-linecap="round"/>
  </svg>
  Records
</a>
      <a href="#utd" class="btn btn-sm d-flex align-items-center gap-2 px-3 text-secondary fw-medium nav-action" style="font-size:13px; border-radius:8px;">
        <svg width="14" height="14" viewBox="0 0 14 14" fill="none">
          <path d="M1.5 9.5l5-5 2 2-5 5H1.5v-2z" stroke="currentColor" stroke-width="1.4" stroke-linecap="round" stroke-linejoin="round"/>
          <path d="M9 3l2 2" stroke="currentColor" stroke-width="1.4" stroke-linecap="round"/>
          <path d="M11.5 1.5l1 1a.7.7 0 010 1l-.7.7-2-2 .7-.7a.7.7 0 011 0z" stroke="currentColor" stroke-width="1.3" stroke-linecap="round"/>
        </svg>
        Update
      </a>
      <a href="#dlt" class="btn btn-sm d-flex align-items-center gap-2 px-3 text-secondary fw-medium nav-action-danger" style="font-size:13px; border-radius:8px;">
        <svg width="14" height="14" viewBox="0 0 14 14" fill="none">
          <path d="M2 4h10M5 4V2h4v2M6 7v4M8 7v4M3 4l.7 7.3A1 1 0 004.7 12h4.6a1 1 0 001-.7L11 4" stroke="currentColor" stroke-width="1.3" stroke-linecap="round" stroke-linejoin="round"/>
        </svg>
        Delete
      </a>
    </div>
  </div>
</nav>
<br><br>
    <PostData id="pstd" @update="update"></PostData>
    <ReadData id="vwd" ref="readupdate"></ReadData>
    <UpdateData id="utd" @updatey="update" ref="updates" ></UpdateData>
    <DeleteData id="dlt" ref="deletes" @refresh="update"></DeleteData>
  </div>
</template>

<script>
import ReadData from './components/ReadData.vue'
import PostData from './components/PostData.vue'
import UpdateData from './components/UpdateData.vue'
import DeleteData from './components/DeleteData.vue'

export default {
  components: {
    ReadData,PostData,UpdateData,DeleteData
  },
  methods:{
    update(){
      console.log("there should be an update");
      this.$refs.readupdate.update();
      this.$refs.updates.fetchData();
      this.$refs.deletes.fetchData();
    }
  }
}

</script>

<style>
  .nav-action {
    transition: background 0.15s, color 0.15s;
    background: transparent;
    border: 1px solid transparent;
  }
  .nav-action:hover, .nav-action.active {
    background: #f1f3f5;
    color: #212529 !important;
    border-color: #dee2e6;
    text-decoration: none;
  }
  .nav-action-danger {
    transition: background 0.15s, color 0.15s;
    background: transparent;
    border: 1px solid transparent;
  }
  .nav-action-danger:hover, .nav-action-danger.active {
    background: #fff5f5;
    color: #dc3545 !important;
    border-color: #f5c6cb;
    text-decoration: none;
  }
</style>