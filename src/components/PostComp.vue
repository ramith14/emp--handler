<template>
    <div>
    <h1>Form for filling employee details</h1>
    <form @submit="postData" method="post">
        Emp_ID: <input type="text" name="emp_id" placeholder="emp_id" v-model="postd.emp_id"><br><br/>
        Emp_name: <input type="text" name="title" placeholder="name" v-model="postd.emp_name"><br><br/>
        Designation: <input type="text" name="desg" placeholder="Desg" v-model="postd.designation"><br><br/>
        Salary: <input type="number" name="salary" placeholder="salary" v-model="postd.salary"><br><br/>
        Dept: <input type="text" name="dept" placeholder="price" v-model="postd.dept"><br><br/>
        <button type="submit">Post</button>
    </form>
</div>
</template>
<script>
import axios from 'axios';

export default {
    name: "PostComp",
    data() {
        return {
            postd: {
                emp_id: null,
                emp_name: null,
                designation: null,
                salary: null,
                dept: null
            }
        }
    },
    methods: {
        postData(e) {
            axios.post("https://69e857332f51b534be5fecf8.mockapi.io/api/12/employedb", {
                emp_id: this.postd.emp_id,
                emp_name: this.postd.emp_name,
                designation: this.postd.designation,
                salary: this.postd.salary,
                dept: this.postd.dept
            })
                .then(res => console.log(res.data)).catch(err => console.log(err));
            e.preventDefault();
        }
    }
}
</script>