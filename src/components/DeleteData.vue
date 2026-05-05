<template>
  <div class="container py-5" style="max-width: 860px;">
    <div class="card border shadow-sm rounded-3 p-4">

      <!-- Header -->
      <div class="d-flex align-items-center gap-3 mb-4">
        <div class="d-flex align-items-center justify-content-center rounded-2 bg-danger bg-opacity-10" style="width:40px;height:40px;flex-shrink:0;">
          <svg width="18" height="18" viewBox="0 0 14 14" fill="none">
            <path d="M2 4h10M5 4V2h4v2M6 7v4M8 7v4M3 4l.7 7.3A1 1 0 004.7 12h4.6a1 1 0 001-.7L11 4" stroke="#dc3545" stroke-width="1.3" stroke-linecap="round" stroke-linejoin="round"/>
          </svg>
        </div>
        <div>
          <h5 class="mb-0 fw-semibold">Delete Employee</h5>
          <p class="mb-0 text-muted" style="font-size:13px;">{{ datas.length }} employees in database</p>
        </div>
      </div>

      <hr class="mt-0 mb-3">

      <!-- Empty State -->
      <div v-if="!datas.length" class="text-center py-5">
        <svg width="40" height="40" viewBox="0 0 16 16" fill="none" class="mb-3">
          <circle cx="8" cy="5" r="3" stroke="#adb5bd" stroke-width="1.2"/>
          <path d="M2 13c0-3.314 2.686-5 6-5s6 1.686 6 5" stroke="#adb5bd" stroke-width="1.2" stroke-linecap="round"/>
        </svg>
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
            <tr v-for="item in datas" :key="item.emp_id">

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
                <button @click="deleteItem(item)"
                  class="btn btn-outline-danger btn-sm d-flex align-items-center gap-1 px-3"
                  style="font-size:12px;border-radius:6px;">
                  <svg width="12" height="12" viewBox="0 0 14 14" fill="none">
                    <path d="M2 4h10M5 4V2h4v2M6 7v4M8 7v4M3 4l.7 7.3A1 1 0 004.7 12h4.6a1 1 0 001-.7L11 4"
                      stroke="currentColor" stroke-width="1.3" stroke-linecap="round" stroke-linejoin="round"/>
                  </svg>
                  Delete
                </button>
              </td>

            </tr>
          </tbody>
        </table>
      </div>

    </div>
  </div>
</template>
<script>
import axios from 'axios'

export default{
    name:"DeleteData",
    data(){
        return {
            datas:[]
        }
    },
    mounted(){
        this.fetchData();
    },
    methods:{
        async fetchData()
            {
                console.log("update from delete");
        await axios.get("https://69e857332f51b534be5fecf8.mockapi.io/api/12/employedb").then((da) => this.datas=da.data).catch((er) => console.log(er));
        },
        deleteItem(item){
            axios.delete(`https://69e857332f51b534be5fecf8.mockapi.io/api/12/employedb/${item.id}`).then(r => console.log(r),er => console.log(er));
            this.$emit("refresh");
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
/* Heading */
h3 {
margin-bottom: 20px;
color: #db2121;
}
/* Table styling */
.em-table {
width: 100%;
box-shadow: 0 2px 8px rgba(0,0,0,0.1);
}
/* Header */
.em-table th {
background-color: #3498db;
color: white;
padding: 10px;
}
/* Table cells */
.em-table td {
padding: 10px;
border-bottom: 1px solid #ddd;
}
/* Zebra striping */
.em-table tr:nth-child(even) {
    background-color: #f9f9f9;
}
/* Hover effect */
.em-table tr:hover {
background-color: #f1f1f1;
}
.em-table button{
    margin-top:5px;
    background-color:red;
    border:0px;
    padding:5px;
    color:white;
    cursor:pointer;
}
</style>