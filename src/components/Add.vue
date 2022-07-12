<template>
    <Header />
    <h1>Here we add new Project</h1>
    <form action="" class="add">
        <input v-model="project.name" type="text" name="name" placeholder="Project Nshya" id="">
        <input v-model="project.purpose" type="text" name="purpose" placeholder="Intego ya Project" id="">
        <input v-model="project.time" type="text" name="time" placeholder="Igihe giteganyijwe" id="">
        <button @click="addproject" type="button">Add New project</button>
    </form>
</template>
<script>
import Header from './Header.vue'
import axios from 'axios'
export default {
    name: "AddView",
    components: {
        Header
    },
    data() {
        return {
            project: {
                name: '',
                purpose: '',
                time: '',
                task:1,
                progress:0,
                done:0
            }
        }
    },

    methods: {
        async addproject() {
            let result = await axios.post("http://localhost:3000/project", {
                name: this.project.name,
                purpose: this.project.purpose,
                time: this.project.time,
                task: this.project.task,
                progress: this.project.progress,
                done: this.project.done
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