<template>
  <div class="container py-5" style="max-width: 540px;">
    <div class="card border shadow-sm rounded-3 p-4">
      <div class="d-flex align-items-center gap-3 mb-4">
        <div class="d-flex align-items-center justify-content-center rounded-2 bg-primary bg-opacity-10" style="width:40px;height:40px;flex-shrink:0;">
          <svg width="20" height="20" viewBox="0 0 16 16" fill="none">
            <circle cx="8" cy="5" r="3" fill="#0d6efd"/>
            <path d="M2 13c0-3.314 2.686-5 6-5s6 1.686 6 5" stroke="#0d6efd" stroke-width="1.5" stroke-linecap="round"/>
          </svg>
        </div>
        <div>
          <h5 class="mb-0 fw-semibold">Add Employee</h5>
          <p class="mb-0 text-muted" style="font-size:13px;">Fill in the details to add a new record</p>
        </div>
      </div>
      <hr class="mb-4 mt-0">
      <form @submit.prevent="postData">
        <div class="row g-3 mb-3">
          <div class="col-5">
            <label class="form-label text-muted fw-medium" style="font-size:13px;">Employee ID</label>
            <input
              type="text"
              class="form-control form-control-sm"
              placeholder="e.g. EMP001"
              v-model="postd.emp_id"
            />
          </div>
          <div class="col-7">
            <label class="form-label text-muted fw-medium" style="font-size:13px;">Full Name</label>
            <input
              type="text"
              class="form-control form-control-sm"
              placeholder="e.g. John Smith"
              v-model="postd.emp_name"
            />
          </div>
        </div>
        <div class="mb-3">
          <label class="form-label text-muted fw-medium" style="font-size:13px;">Designation</label>
          <input
            type="text"
            class="form-control form-control-sm"
            placeholder="e.g. Software Engineer"
            v-model="postd.designation"
          />
        </div>
        <div class="row g-3 mb-4">
          <div class="col-6">
            <label class="form-label text-muted fw-medium" style="font-size:13px;">Salary (₹)</label>
            <input
              type="number"
              class="form-control form-control-sm"
              placeholder="e.g. 50000"
              v-model="postd.salary"
            />
          </div>
          <div class="col-6">
            <label class="form-label text-muted fw-medium" style="font-size:13px;">Department</label>
            <input
              type="text"
              class="form-control form-control-sm"
              placeholder="e.g. Engineering"
              v-model="postd.dept"
            />
          </div>
        </div>
        <div v-if="alert.show"
  :class="`alert alert-${alert.type} d-flex align-items-center justify-content-between py-2 px-3 mb-3`"
  style="font-size:13px; border-radius:8px;">
  {{ alert.message }}
  <button type="button" class="btn-close" style="font-size:10px;" @click="alert.show = false"></button>
</div>
        <div class="d-flex gap-2">
          <button type="submit" class="btn btn-primary btn-sm px-4 d-flex align-items-center gap-2">
            <svg width="14" height="14" viewBox="0 0 14 14" fill="none">
              <path d="M7 1v12M1 7h12" stroke="white" stroke-width="1.8" stroke-linecap="round"/>
            </svg>
            Add Employee
          </button>
          <button type="reset" class="btn btn-sm px-4 text-secondary" style="border:1px solid #dee2e6;">
            Clear
          </button>
        </div>
      </form>
    </div>
  </div>
</template>
<script>
import axios from 'axios'

export default{
    name:"PostData",
    data(){
        return{
            postd:{
                emp_id:null,
                emp_name:null,
                designation:null,
                salary:null,
                dept:null
            },
            alert: {
  show: false,
  type: 'success',
  message: ''
}
        }
    }
    ,methods:{
        postData(e){
            axios.post("https://69e857332f51b534be5fecf8.mockapi.io/api/12/employedb",{
                emp_id: this.postd.emp_id,
                emp_name: this.postd.emp_name,
                designation: this.postd.designation,
                salary: this.postd.salary,
                dept: this.postd.dept
            }).then(r => console.log(r.data)).catch(e => console.log(e));
            e.preventDefault();
            this.$emit("update");
             this.showAlert('success', 'Employee added successfully!')
        }
        ,showAlert(type, message) {
  this.alert = { show: true, type, message }
  setTimeout(() => { this.alert.show = false }, 4000)
}
    }
}
</script>

<style scoped>

.container {
width: 70%;
margin: 40px auto;
text-align: center;
font-family: Arial, sans-serif;
}
h3 {
margin-bottom: 20px;
color: rgb(230, 53, 80);
}
</style>