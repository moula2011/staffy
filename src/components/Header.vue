<template>
    <div class="nav">
        <router-link to="/">Home</router-link>
        <router-link to="/add">Add Project</router-link>
        <router-link to="/update">Update Project</router-link>
        <a @click="logout" href="#">Logout</a>
    </div>
</template>

<script>
export default {
    name: "HeaderView",
    methods: {
        logout()
        {
            localStorage.clear()
            this.$router.push({name:'Login'})
        }
    }

}
</script>
<style>
.nav{
    background-color: #333;
    overflow: hidden;
    box-shadow: 0px 0px 18px 0px #333;
}
.nav a{
    float: left;
    color: white;
    padding: 16px 14px;
    text-decoration: none;
    margin-right: 5px;
}
.nav a:hover{
    background-color: #ddd;
    color: #333;
}
</style>