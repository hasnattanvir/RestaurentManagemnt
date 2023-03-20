<template>
    <div class="signupbox">
        <img src="../assets/logo.png" alt="photo"/>
        <h1>Login</h1>

        <div class="registerbox">
            <div class="inputbox">
                <input type="email" v-model="email" placeholder="Enter Your Email">
            </div>
            <div class="inputbox">
                <input type="password" v-model="password" placeholder="Enter Your Password">
            </div>
            <div class="inputbox">
                <button type="submit" v-on:click="logIn" class="btn">Login</button>
            </div>
            <p>
                <router-link to="/signup">Sign Up</router-link>
            </p>
        </div>
    </div>
</template>

<script>
import axios from 'axios';
export default{
    name:'Login',
    data(){
        return{
            email:'',
            password:'',
        }
    },
    methods:{
        async logIn(){
            let result = await axios.get(
                `http://localhost:3000/user?email=${this.email}&password=${this.password}`
                )

            if(result.status == 200 && result.data.length > 0){
                localStorage.setItem("user.info",JSON.stringify(result.data[0]));
                this.$router.push({name:'Home'});
                // alert("login in success");
            }
        }
    },
    mounted(){
        let user = localStorage.getItem('user.info');
        if(user){
            this.$router.push({name:'Home'})
        }
    }

}
</script>

<style scoped>
.signupbox{
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