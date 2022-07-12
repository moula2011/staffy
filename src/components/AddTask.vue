<template>
    <Header />
    <h1>Here we add new task</h1>
    <form action="" class="add">
        <input v-model="task.name" type="text" name="name" placeholder="Task Nshya" id="">
        <input v-model="task.purpose" type="text" name="purpose" placeholder="Intego ya Task" id="">
        <input v-model="task.time" type="text" name="time" placeholder="Igihe giteganyijwe" id="">
        <button @click="addtask" type="button">Add New Task</button>
    </form>
</template>
<script>
import Header from './Header.vue'
import axios from 'axios'
export default {
    name: "AddTask",
    components: {
        Header
    },
    data() {
        return {
            task: {
                name: '',
                purpose: '',
                time: ''
                
            }
        }
    },

    methods: {
        async addtask() {
            let result = await axios.post("http://localhost:3000/task", {
                name: this.task.name,
                purpose: this.task.purpose,
                time: this.task.time
            })
            console.warn("Result", result)
            if (result.status == 201) {
                // localStorage.setItem("user-info", JSON.stringify(result.data))
                this.$router.push({ name: 'Home' })
            }
        }
    },

    mounted() {
        let user = localStorage.getItem('user-info')
        if (!user) {
            this.$router.push({ name: 'SignUp' })
        }
    }
}
</script>