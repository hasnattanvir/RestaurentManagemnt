<template>
    <div>
        <Header />
        <div class="updateres">
            <h3>Update Restaurant Page</h3>
            <div class="inputbox">
                <input type="text" v-model="restaurant.name" placeholder="Restaurant Name">
            </div>
            <div class="inputbox">
                <input type="text" v-model="restaurant.address" placeholder="Restaurant Address">
            </div>
            <div class="inputbox">
                <input type="text" v-model="restaurant.contact" placeholder="Contact Number">
            </div>
            <div class="inputbox">
                <button type="submit" v-on:click="updateRestaurent" class="btn">Update Restaurant</button>
            </div>

        </div>
    </div>
</template>


<script>
    import axios from 'axios';
    import Header from './Header.vue';
    export default {
        name: 'Update',
        data() {
            return {
                restaurant: {
                    name: '',
                    address: '',
                    contact: '',
                }
            }
        },
        methods: {
            async updateRestaurent() {
                // console.warn(this.restaurant);
                // http://localhost:3000/restaurant/1/
                // put
                const result = await axios.put("http://localhost:3000/restaurant/" + this.$route.params.id, {
                    name: this.restaurant.name,
                    address: this.restaurant.address,
                    contact: this.restaurant.contact,
                });
                if(result.status == 200){
                    this.$router.push({name:'Home'});
                }
            }
        },
        async mounted() {
            let user = localStorage.getItem('user.info');
            if (!user) {
                this.$router.push({
                    name: 'Signup'
                })
            }

            const result = await axios.get("http://localhost:3000/restaurant/" + this.$route.params.id);

            // console.warn(this.$route.params.id);
            // console.warn(result);
            this.restaurant = result.data
        },
        components: {
            Header,
        }
    }
</script>

<style scoped>
    .updateres {
        padding-top: 20px;
        width: 1300px;
        max-width: 100%;
        margin: auto;
        display: flex;
        justify-content: center;
        align-items: center;
        flex-direction: column;
    }

    h1 {
        padding-top: 30px;
    }

    img {
        width: 150px;
    }

    .inputbox {
        padding-top: 10px;
        width: 320px;
        padding-bottom: 7px;
    }

    .inputbox input {
        width: 100%;
        height: 30px;
    }

    .inputbox .btn {
        padding: 6px 15px;
        cursor: pointer;
    }
</style>