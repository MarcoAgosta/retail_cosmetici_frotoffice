<template>
<div class="background-purple">
    <Navbar></Navbar>
    <div class="container">
        <h1>Profumi in catalogo</h1>
        <div class="row gx-3">
            <div v-for="perfume in perfumes" class="col-12 col-sm-6 col-md-4 col-xl-3 p-2">
                <div class="d-flex flex-column align-items-center border bg-light carta justify-content-between p-2">
                    <img :src="backendURL + perfume.product_img" class="h-75 img-carta" alt="">
                    <h4 class="m-0 text-center purple">{{ perfume.name }}</h4>
                </div>
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
    padding-top: 96px;
}
.carta{
    height: 250px;
}
.img-carta{
    max-width: 100%;
}

.purple{
    color: purple;
}
</style>