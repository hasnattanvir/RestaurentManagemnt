<template>
    <div>
    <Header/>
        <h1>Home Page</h1>
        <table>
            <tr>
                <th>Name</th>
                <th>Address</th>
                <th>Contact No</th>
                <th>Action</th>
            </tr>
            <tr v-for="item in restaurants" :key="item">
                <td>{{ item.name }}</td>
                <td>{{ item.address }}</td>
                <td>{{ item.contact }}</td>
                <td>
                    <router-link :to="'/Update/'+item.id">Edit</router-link> | 
                    <button v-on:click="deleteRestaurant(item.id)">Delete</button>
                </td>
            </tr>
        </table>
    </div>
</template>

<script>
import axios from 'axios';
import Header from './Header.vue';

export default{
    name:'Home',
    data(){
        return{
            name:'',
            restaurants:[],
        }
    },
    components:{
        Header,
    },
    methods:{
       async deleteRestaurant(id){
            // console.warn(id);
            let result = await axios.delete("http://localhost:3000/restaurant/"+id);
            if(result.status===200){
                this.loadPage();
            }
        },

       async loadPage(){
            let user = localStorage.getItem('user.info');
            if(!user){
                this.$router.push({name:'Signup'})
            }
            //user name show
            this.name = JSON.parse(user).name
            let result = await axios.get("http://localhost:3000/restaurant");
            this.restaurants = result.data
        }
    },

    mounted(){
        this.loadPage();
    },
}
</script>

<style scoped>
    table{
        width: 100%;
    }
    table,td,th{
        border: 1px solid green;
        border-collapse: collapse;
    }
</style>