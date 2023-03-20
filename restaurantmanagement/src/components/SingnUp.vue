<template>
    <div class="signupbox">
        <img src="../assets/logo.png" alt="photo"/>
        <h1>Sign Up</h1>

        <div class="registerbox">
            <div class="inputbox">
                <input type="text" v-model="name" placeholder="Enter Your Name">
            </div>
            <div class="inputbox">
                <input type="email" v-model="email" placeholder="Enter Your Email">
            </div>
            <div class="inputbox">
                <input type="password" v-model="password" placeholder="Enter Your Password">
            </div>
            <div class="inputbox">
                <input type="text" v-model="phone" placeholder="Enter Your Phone">
            </div>
            <div class="inputbox">
                <button type="submit" v-on:click="singUP" class="btn">Create Account</button>
            </div>
            <p>
                <router-link to="/login">Login</router-link>
            </p>
        </div>
    </div>
</template>

<script>
import axios from 'axios'
export default{
    name:'Signup',
    data(){
        return{
            name:'',
            email:'',
            password:'',
            phone:'',
        }
    },
    methods:{
        async singUP(){
            // console.warn("singup",this.name,this.email,this.password,this.phone)
            let result= await axios.post("http://localhost:3000/user",{
                name:this.name,
                email:this.email,
                password:this.password,
                phone:this.phone,
            });
           
            if(result.status==201){
                localStorage.setItem("user.info",JSON.stringify(result.data));
                this.$router.push({name:'Home'})
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