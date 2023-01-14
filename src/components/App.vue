<template>
    <div>
        <input type="text" name="search" v-model="search"><br>
        <table class="table table-dark">
            <tr v-for="item in students" v-bind:key="item.id">
                <td>{{ item.name }}</td>
                <td><input type="checkbox" v-model="item.isDonePr"></td>
                <td>{{ item.group }}</td>
                <td><a href="#" @click="deleteStudent(item.id)">Видалити</a></td>
            </tr>
        </table>

        <input v-model="student.name">
        <input type="checkbox" v-model="student.isDonePr">
        <select v-model="student.group">
            <option value="RPZ 19 1/9">RPZ 19 1/9</option>
            <option value="RPZ 19 2/9">RPZ 19 2/9</option>
        </select>
        <button @click="addStudent()">Add student</button>
    </div>
</template>
 
<script>
import axios from 'axios'

export default {
    data() {
        return {
            students: [],
            student: { "name": "", isDonePr: false, group: "" },
            newmark: '',
            newground: '',
            newIsDonePr: '',
            newname: '',
            search: '',
            piece: '',
        }
    },
    mounted() {
        axios.get("http://34.82.81.113:3000/students").then((response) => {
            console.log(response.data);
            this.students = response.data;
        })
    },
    methods: {
        deleteStudent(studId) {
            axios.delete(`http://34.82.81.113:3000/students/${studId}`)
            .then(data => {
         console.log(data);
})

        },
        addStudent() {
            axios.post("http://34.82.81.113:3000/students", {
                name: this.student.name,
                group: this.student.group,
                isDonePr: this.student.isDonePr
            })
                .then(data => {
                    console.log(data);
                })

            
        }
    }
}
</script>
