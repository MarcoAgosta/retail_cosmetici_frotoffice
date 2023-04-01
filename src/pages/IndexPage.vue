<template>
<div class="background-purple">
    <Navbar></Navbar>
    <div class="container pt-4">
        <h1>Profumi in catalogo</h1>
        <div class="row g-3">
            <div v-for="perfume in perfumes" class="col-4 p-3 d-flex flex-column align-items-center perfume">
                <img :src="backendURL + perfume.product_img" class="w-50" alt="">
                <h4>{{ perfume.name }}</h4>
            </div>
        </div>
    </div>
</div>
</template>

<script>
import Navbar from "../components/Navbar.vue";
import { reactive } from "vue";
import axios from "axios";
export default{
    data(){
        return{
            perfumes:[],
            backendURL:"http://127.0.0.1:8000/storage/"
        }
    },
    components:{Navbar},
    methods:{
        fetchAllPerfumes(){
            axios.get("http://localhost:8000/api/perfumes").then((resp)=>{
                console.log(resp)
                this.perfumes=resp.data.results
                })
        },
    },
    mounted(){
        this.fetchAllPerfumes()
    }
    }
</script>

<style scoped>
.background-purple{
background-color: purple;
min-height: 100vh;
}
.container{
    background-color: white;
}
.perfume{
border: 1px solid darkgray;
}
</style>