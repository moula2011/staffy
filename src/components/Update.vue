<template>
    <Header />
    <h1>Hello this is Update page</h1>
    <form action="" class="add">
        <input v-model="project.name" type="text" name="name" placeholder="Enter Name" id="">
        <input v-model="project.purpose" type="text" name="purpose" placeholder="Enter purpose" id="">
        <input v-model="project.time" type="text" name="time" placeholder="Enter time" id="">
        <button @click="updateproject" type="button">Update project</button>
    </form>
</template>
<script>
import Header from './Header.vue'
import axios from 'axios'

export default {
    name: "UpDate",
    components: {
        Header
    },
    data() {
        return {
            project: {
                name: '',
                purpose: '',
                time: ''
            }
        }
    },
    methods: {
        async updateproject() {
            console.warn(this.project)
            const result = await axios.put("http://localhost:3000/project/"+this.$route.params.id, {
                name: this.project.name,
                purpose: this.project.purpose,
                time: this.project.time
            })
            if (result.status == 200) {
                // localStorage.setItem("user-info", JSON.stringify(result.data))
                this.$router.push({ name: 'Home' })
            }
        }
    },
    async mounted() {
        let user = localStorage.getItem('user-info')
        if (!user) {
            this.$router.push({ name: 'SignUp' })
        }
        const result = await axios.get('http://localhost:3000/project/'+this.$route.params.id)
        console.warn(result)
        this.project = result.data
    }
}
</script>