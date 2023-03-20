<template>
    <div>
        <Header />
        <div class="addresta">
            <h3>Add Restaurant Page</h3>
            <div class="inputbox">
                <input type="text" v-model="restaurantname" placeholder="Restaurant Name">
            </div>
            <div class="inputbox">
                <input type="text" v-model="restaurantadd" placeholder="Restaurant Address">
            </div>
            <div class="inputbox">
                <input type="text" v-model="restaurantphone" placeholder="Contact Number">
            </div>
            <div class="inputbox">
                <button type="submit" v-on:click="addRestaurent" class="btn">Add Restaurant</button>
            </div>
           
        </div>
    </div>
</template>

<script>
    import axios from 'axios';
    import Header from './Header.vue';

    export default {
        name: 'Add',
        data(){
            return{
                restaurantname:'',
                restaurantadd:'',
                restaurantphone:'',
            }
        },
        mounted() {
            let user = localStorage.getItem('user.info');
            if (!user) {
                this.$router.push({
                    name: 'Signup'
                })
            }
        },
        components: {
            Header,
        },
        methods:{
            async addRestaurent(){
                let result= await axios.post("http://localhost:3000/restaurant",{
                name:this.restaurantname,
                address:this.restaurantadd,
                password:this.password,
                contact:this.restaurantphone,
                });
                // console.warn(result);
            }
        }
    }
</script>

<style scoped>
.addresta{
        padding-top: 20px;
        width:1300px;
        max-width: 100%;
        margin: auto;
        display: flex;
        justify-content: center;
        align-items: center;
        flex-direction: column;
    }
    h1{
        padding-top: 30px;
    }
    img{
        width: 150px;
    }
    .inputbox{
        padding-top: 10px;
        width: 320px;
        padding-bottom: 7px;
    }
    .inputbox input{
        width: 100%;
        height: 30px;
    }
    .inputbox .btn{
        padding: 6px 15px;
        cursor: pointer;
    }
</style>