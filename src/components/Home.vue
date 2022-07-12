;<template>
    <Header />
    <h1>Hello {{ name }}..!! we are working on this Project</h1>
    <table width="98%">
        <tr >
            <th>No</th>
            <th>Project</th>
            <th width="20%">Purpose</th>
            <th>Time</th>  
            <th colspan="3">Tasks</th>
            <!-- <th>%</th> -->
            <th colspan="4">Actions</th>
        </tr>

        <tr v-for="item in project" :key="item.id">
            <td>{{ item.id }}</td>
            <td>{{ item.name }}</td>
            <td>{{ item.purpose }}</td>
            <td>{{ item.time }}</td>
            <td>{{ item.progress }} In progress</td>
            <td>{{ item.done }} Done</td>
            <td>{{((100 * item.done)/item.task) }} %</td>
            <td>
                <router-link :to="'/Update/' + item.id" style="text-decoration:none;"><span style="border:1px solid indigo; padding:5px; border-radius:4px 4px 4px 4px;">Update</span></router-link>
            </td>
            <td>
                <router-link :to="'/Update/' + item.id" style="text-decoration:none;"><span style="border:1px solid indigo; padding:5px; border-radius:4px 4px 4px 4px;">Tasks</span></router-link>
            </td>
            <td>
                <router-link :to="'/Update/' + item.id" style="text-decoration:none;"><span style="border:1px solid indigo; padding:5px; border-radius:4px 4px 4px 4px;">Idea</span></router-link>
            </td>
            <td>
                <button @click="deleteproject(item.id)" style=" padding:5px;">Delete</button>
            </td>
        </tr>
    </table>
</template>
<script>
import Header from './Header.vue'
import axios from 'axios'
export default {
    name: "HomeView",
    components: {
        Header
    },
    data() {
        return {
            name: '',
            project: []
        }
    },
    methods: {
        async deleteproject(id) {

            let result = await axios.delete("http://localhost:3000/project/" + id)
            console.warn(id)
            if (result.status == 200) {
                this.loadData()
            }
        },
        async loadData() {
            let user = localStorage.getItem('user-info')
            this.name = JSON.parse(user).name
            if (!user) {
                this.$router.push({ name: 'SignUp' })
            }
            let result = await axios.get("http://localhost:3000/project")
            console.warn(result)
            this.project = result.data
        }
    },
    async mounted() {
        this.loadData()
    }
}
</script>
<style>
table {
    border-collapse: collapse;
    margin: 18px 16px;
}

td,
th {
    border: 1px solid #333;
    padding: 5px 10px;
}
</style>