<template>
<div class="background-purple">
    <Navbar></Navbar>
    <div class="container">
        <div v-if="perfumes[0]" class="row gx-3">
            <h1 class="purple">Profumi in catalogo</h1>
            <div v-for="perfume in perfumes" class="col-6 col-md-4 col-xl-3 p-2">
                <div class="d-flex flex-column carta justify-content-between p-2">
                    <div class="d-flex justify-content-center flex-column">
                        <img :src="backendURL + perfume.product_img" class="w-75 mb-1 img-carta" alt="">
                    </div>

                    <div>
                        <h4 class="m-0 purple">{{ perfume.name }}</h4>
                        <span class="brand">{{ perfume.brand }}</span>
                    </div>
                </div>
            </div>
        </div>
        <div v-else class="d-flex flex-column align-items-center justify-content-center loader-contenitore">
            <div class="loader"></div>
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
background-color: rgba(182, 0, 182, 0.699);
min-height: 100vh;
}
.container{
    background-color: rgb(252, 245, 246);
    padding-top: 96px;
}
.carta{
    max-height: 300px;
}
.img-carta{
    max-width: 100%;
    border-radius: 5%;
}

.purple{
    color: purple;
}

.loader {
  border: 16px solid white; 
  border-top: 16px solid purple; 
  border-radius: 50%;
  width: 120px;
  height: 120px;
  animation: spin 2s linear infinite;
}

@keyframes spin {
  0% { transform: rotate(0deg); }
  100% { transform: rotate(360deg); }
}

.loader-contenitore{
    height: 90vh;
}
.brand{
font-family: initial;
color: gray;
}
</style>