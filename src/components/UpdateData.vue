<template>
  <div class="container py-5" style="max-width: 860px;">

    <!-- Employee Table Card -->
    <div class="card border shadow-sm rounded-3 p-4 mb-4">

      <!-- Header -->
      <div class="d-flex align-items-center gap-3 mb-4">
        <div class="d-flex align-items-center justify-content-center rounded-2 bg-warning bg-opacity-10" style="width:40px;height:40px;flex-shrink:0;">
          <svg width="18" height="18" viewBox="0 0 14 14" fill="none">
            <path d="M1.5 9.5l5-5 2 2-5 5H1.5v-2z" stroke="#ffc107" stroke-width="1.4" stroke-linecap="round" stroke-linejoin="round"/>
            <path d="M9 3l2 2" stroke="#ffc107" stroke-width="1.4" stroke-linecap="round"/>
            <path d="M11.5 1.5l1 1a.7.7 0 010 1l-.7.7-2-2 .7-.7a.7.7 0 011 0z" stroke="#ffc107" stroke-width="1.3" stroke-linecap="round"/>
          </svg>
        </div>
        <div>
          <h5 class="mb-0 fw-semibold">Edit Employee</h5>
          <p class="mb-0 text-muted" style="font-size:13px;">Click Edit on any row to modify the record</p>
        </div>
      </div>

      <hr class="mt-0 mb-3">

      <!-- Empty State -->
      <div v-if="!datas.length" class="text-center py-5">
        <p class="text-muted mb-0" style="font-size:14px;">No employee records found</p>
      </div>

      <!-- Table -->
      <div v-else class="table-responsive">
        <table class="table table-hover align-middle mb-0" style="font-size:14px;">
          <thead>
            <tr style="background:#f8f9fa;">
              <th class="text-muted fw-medium py-2 px-3" style="font-size:12px;text-transform:uppercase;letter-spacing:0.5px;border-bottom:1px solid #dee2e6;">ID</th>
              <th class="text-muted fw-medium py-2 px-3" style="font-size:12px;text-transform:uppercase;letter-spacing:0.5px;border-bottom:1px solid #dee2e6;">Employee</th>
              <th class="text-muted fw-medium py-2 px-3" style="font-size:12px;text-transform:uppercase;letter-spacing:0.5px;border-bottom:1px solid #dee2e6;">Designation</th>
              <th class="text-muted fw-medium py-2 px-3" style="font-size:12px;text-transform:uppercase;letter-spacing:0.5px;border-bottom:1px solid #dee2e6;">Salary</th>
              <th class="text-muted fw-medium py-2 px-3" style="font-size:12px;text-transform:uppercase;letter-spacing:0.5px;border-bottom:1px solid #dee2e6;">Department</th>
              <th class="text-muted fw-medium py-2 px-3" style="font-size:12px;text-transform:uppercase;letter-spacing:0.5px;border-bottom:1px solid #dee2e6;">Action</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="item in datas" :key="item.emp_id"
              :style="editData.emp_id === item.emp_id ? 'background:#fffbeb;' : ''">

              <td class="px-3 py-3">
                <span class="badge bg-primary bg-opacity-10 text-primary fw-medium" style="font-size:12px;border-radius:6px;">
                  {{ item.emp_id }}
                </span>
              </td>

              <td class="px-3 py-3">
                <div class="d-flex align-items-center gap-2">
                  <div class="d-flex align-items-center justify-content-center rounded-circle bg-primary bg-opacity-10 text-primary fw-medium"
                    style="width:32px;height:32px;font-size:12px;flex-shrink:0;">
                    {{ item.emp_name?.charAt(0).toUpperCase() }}
                  </div>
                  <span class="fw-medium">{{ item.emp_name }}</span>
                </div>
              </td>

              <td class="px-3 py-3 text-muted">{{ item.designation }}</td>

              <td class="px-3 py-3">
                <span class="badge bg-success bg-opacity-10 text-success fw-medium" style="font-size:12px;border-radius:6px;">
                  ₹{{ Number(item.salary).toLocaleString('en-IN') }}
                </span>
              </td>

              <td class="px-3 py-3">
                <span class="badge bg-secondary bg-opacity-10 text-secondary fw-medium" style="font-size:12px;border-radius:6px;">
                  {{ item.dept }}
                </span>
              </td>

              <td class="px-3 py-3">
                <button @click="editButton(item)"
                  class="btn btn-sm d-flex align-items-center gap-1 px-3"
                  :class="editData.emp_id === item.emp_id ? 'btn-warning text-white' : 'btn-outline-warning'"
                  style="font-size:12px;border-radius:6px;">
                  <svg width="12" height="12" viewBox="0 0 14 14" fill="none">
                    <path d="M1.5 9.5l5-5 2 2-5 5H1.5v-2z" stroke="currentColor" stroke-width="1.4" stroke-linecap="round" stroke-linejoin="round"/>
                    <path d="M11.5 1.5l1 1a.7.7 0 010 1l-.7.7-2-2 .7-.7a.7.7 0 011 0z" stroke="currentColor" stroke-width="1.3" stroke-linecap="round"/>
                  </svg>
                  {{ editData.emp_id === item.emp_id ? 'Editing' : 'Edit' }}
                </button>
              </td>

            </tr>
          </tbody>
        </table>
      </div>
    </div>

    <!-- Edit Form Card -->
    <transition name="slide-fade">
      <div v-if="editData.emp_id" class="card border shadow-sm rounded-3 p-4">

        <!-- Edit Form Header -->
        <div class="d-flex align-items-center justify-content-between mb-4">
          <div class="d-flex align-items-center gap-3">
            <div class="d-flex align-items-center justify-content-center rounded-circle bg-warning bg-opacity-10"
              style="width:40px;height:40px;flex-shrink:0;font-size:13px;font-weight:500;color:#ffc107;">
              {{ editData.emp_name?.charAt(0).toUpperCase() }}
            </div>
            <div>
              <h5 class="mb-0 fw-semibold">Editing — {{ editData.emp_name }}</h5>
              <p class="mb-0 text-muted" style="font-size:13px;">ID: {{ editData.emp_id }}</p>
            </div>
          </div>
          <button class="btn btn-sm text-muted" style="border:1px solid #dee2e6;border-radius:6px;" @click="editData = {}">
            Cancel
          </button>
        </div>

        <hr class="mt-0 mb-4">

        <form @submit.prevent="updateData">
          <!-- Row: ID + Name -->
          <div class="row g-3 mb-3">
            <div class="col-5">
              <label class="form-label text-muted fw-medium" style="font-size:13px;">Employee ID</label>
              <input type="text" class="form-control form-control-sm" v-model="editData.emp_id" placeholder="e.g. EMP001"/>
            </div>
            <div class="col-7">
              <label class="form-label text-muted fw-medium" style="font-size:13px;">Full Name</label>
              <input type="text" class="form-control form-control-sm" v-model="editData.emp_name" placeholder="e.g. John Smith"/>
            </div>
          </div>

          <!-- Designation -->
          <div class="mb-3">
            <label class="form-label text-muted fw-medium" style="font-size:13px;">Designation</label>
            <input type="text" class="form-control form-control-sm" v-model="editData.designation" placeholder="e.g. Software Engineer"/>
          </div>

          <!-- Row: Salary + Dept -->
          <div class="row g-3 mb-4">
            <div class="col-6">
              <label class="form-label text-muted fw-medium" style="font-size:13px;">Salary (₹)</label>
              <input type="number" class="form-control form-control-sm" v-model="editData.salary" placeholder="e.g. 50000"/>
            </div>
            <div class="col-6">
              <label class="form-label text-muted fw-medium" style="font-size:13px;">Department</label>
              <input type="text" class="form-control form-control-sm" v-model="editData.dept" placeholder="e.g. Engineering"/>
            </div>
          </div>

          <!-- Actions -->
          <div class="d-flex gap-2">
            <button type="submit" class="btn btn-warning btn-sm px-4 text-white d-flex align-items-center gap-2">
              <svg width="13" height="13" viewBox="0 0 14 14" fill="none">
                <path d="M1.5 9.5l5-5 2 2-5 5H1.5v-2z" stroke="white" stroke-width="1.4" stroke-linecap="round" stroke-linejoin="round"/>
                <path d="M11.5 1.5l1 1a.7.7 0 010 1l-.7.7-2-2 .7-.7a.7.7 0 011 0z" stroke="white" stroke-width="1.3" stroke-linecap="round"/>
              </svg>
              Update Employee
            </button>
            <button type="button" class="btn btn-sm px-4 text-secondary" style="border:1px solid #dee2e6;" @click="editData = {}">
              Cancel
            </button>
          </div>
        </form>

      </div>
    </transition>

  </div>
</template>

<script>
import axios from 'axios'

export default{
    name:"UpdateData",
    data(){
        return {
            datas:[],
            editData:{
                id:null
            }
        }
    },
    mounted(){
        this.fetchData();
    },
    methods:{
        editButton(item){
            this.editData=item
        },
        async fetchData()
            {
                console.log("update in updateData")
        await axios.get("https://69e857332f51b534be5fecf8.mockapi.io/api/12/employedb").then((da) => this.datas=da.data).catch((er) => console.log(er));
        },
        async updateData(){
           await axios.put(`https://69e857332f51b534be5fecf8.mockapi.io/api/12/employedb/${this.editData.id}`,this.editData).then((da) => this.datas=da.data).catch((er) => console.log(er));
           this.fetchData();
           this.editData={id:null};
           this.$emit("updatey");
        }
    }
}
</script>
<style>
.container {
width: 70%;
margin: 40px auto;
text-align: center;
font-family: Arial, sans-serif;
}
.slide-fade-enter-active {
  transition: all 0.25s ease;
}
.slide-fade-enter-from {
  opacity: 0;
  transform: translateY(-10px);
}
/* Heading */
h3 {
margin-bottom: 20px;
color: #db2121;
}
/* Table styling */
.emp-table {
width: 100%;
box-shadow: 0 2px 8px rgba(0,0,0,0.1);
}
/* Header */
.emp-table th {
background-color: #3498db;
color: white;
padding: 10px;
}
/* Table cells */
.emp-table td {
padding: 10px;
border-bottom: 1px solid #ddd;
}
/* Zebra striping */
.emp-table tr:nth-child(even) {
    background-color: #f9f9f9;
}
/* Hover effect */
.emp-table tr:hover {
background-color: #f1f1f1;
}
.emp-table button{
    margin-top:5px;
    background-color:greenyellow;
    padding:3px;
    padding-left:10px;
    padding-right:10px;
    cursor:pointer;
}
.edit-box{
    width: 70%;
margin: 40px auto;
text-align: center;
background-color:beige;
border: 5px solid greenyellow;
font-family: Arial, sans-serif;
}
.edit-box input{
    width:30%;
    margin:10px;

}
.edit-box h3{
    margin-bottom:5px;
}
</style>