<template>
  <div class="container py-5" style="max-width: 860px;">
    <div class="card border shadow-sm rounded-3 p-4">

      <!-- Header -->
      <div class="d-flex align-items-center justify-content-between mb-4">
        <div class="d-flex align-items-center gap-3">
          <div class="d-flex align-items-center justify-content-center rounded-2 bg-primary bg-opacity-10" style="width:40px;height:40px;flex-shrink:0;">
            <svg width="20" height="20" viewBox="0 0 16 16" fill="none">
              <circle cx="8" cy="5" r="3" fill="#0d6efd"/>
              <path d="M2 13c0-3.314 2.686-5 6-5s6 1.686 6 5" stroke="#0d6efd" stroke-width="1.5" stroke-linecap="round"/>
            </svg>
          </div>
          <div>
            <h5 class="mb-0 fw-semibold">Employee Records</h5>
            <p class="mb-0 text-muted" style="font-size:13px;">{{ datas.length }} employees in database</p>
          </div>
        </div>
      </div>

      <hr class="mt-0 mb-3">

      <!-- Empty State -->
      <div v-if="!datas.length" class="text-center py-5">
        <svg width="40" height="40" viewBox="0 0 16 16" fill="none" class="mb-3 text-muted">
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
              <th class="text-muted fw-medium py-2 px-3" style="font-size:12px; text-transform:uppercase; letter-spacing:0.5px; border-bottom: 1px solid #dee2e6;">ID</th>
              <th class="text-muted fw-medium py-2 px-3" style="font-size:12px; text-transform:uppercase; letter-spacing:0.5px; border-bottom: 1px solid #dee2e6;">Employee</th>
              <th class="text-muted fw-medium py-2 px-3" style="font-size:12px; text-transform:uppercase; letter-spacing:0.5px; border-bottom: 1px solid #dee2e6;">Designation</th>
              <th class="text-muted fw-medium py-2 px-3" style="font-size:12px; text-transform:uppercase; letter-spacing:0.5px; border-bottom: 1px solid #dee2e6;">Salary</th>
              <th class="text-muted fw-medium py-2 px-3" style="font-size:12px; text-transform:uppercase; letter-spacing:0.5px; border-bottom: 1px solid #dee2e6;">Department</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="item in datas" :key="item.emp_id">

              <!-- ID badge -->
              <td class="px-3 py-3">
                <span class="badge bg-primary bg-opacity-10 text-primary fw-medium" style="font-size:12px; border-radius:6px;">
                  {{ item.emp_id }}
                </span>
              </td>

              <!-- Avatar + Name -->
              <td class="px-3 py-3">
                <div class="d-flex align-items-center gap-2">
                  <div class="d-flex align-items-center justify-content-center rounded-circle bg-primary bg-opacity-10 fw-medium text-primary"
                    style="width:32px;height:32px;font-size:12px;flex-shrink:0;">
                    {{ item.emp_name?.charAt(0).toUpperCase() }}
                  </div>
                  <span class="fw-medium">{{ item.emp_name }}</span>
                </div>
              </td>

              <!-- Designation -->
              <td class="px-3 py-3 text-muted">{{ item.designation }}</td>

              <!-- Salary -->
              <td class="px-3 py-3">
                <span class="badge bg-success bg-opacity-10 text-success fw-medium" style="font-size:12px; border-radius:6px;">
                  ₹{{ Number(item.salary).toLocaleString('en-IN') }}
                </span>
              </td>

              <!-- Department -->
              <td class="px-3 py-3">
                <span class="badge bg-secondary bg-opacity-10 text-secondary fw-medium" style="font-size:12px; border-radius:6px;">
                  {{ item.dept }}
                </span>
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
    name:"ReadData",
    data(){
        return {
            datas:[]
        }
    },
    async mounted(){
        await axios.get("https://69e857332f51b534be5fecf8.mockapi.io/api/12/employedb").then((da) => this.datas=da.data).catch((er) => console.log(er));
    },
    methods:{
        update(){
            console.log("update from readdata");
            axios.get("https://69e857332f51b534be5fecf8.mockapi.io/api/12/employedb").then((da) => this.datas=da.data).catch((er) => console.log(er));
        }
    }
}
</script>

<style scoped>
/* Page container */
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
</style>
