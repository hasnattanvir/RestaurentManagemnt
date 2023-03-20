<template>
    <div class="menu">
        <router-link  to="/">Home</router-link>
        <router-link  to="Add">Add Restaurant</router-link>
        <!-- <router-link  to="Update">Update Restaurant</router-link> -->
        <a href="#" v-on:click="logout" class="btn">Logout</a>
    </div>
</template>

<script>
export default{
    name:'Header',
    methods:{
        logout(){
            localStorage.clear();
            this.$router.push({name:'Login'});
            // console.log("logout");
        }
    }
}
</script>

<style scoped>
.menu{
    width: 1200px;
    max-width: 100%;
}
.menu a{
    padding: 5px 10px;
}
</style>