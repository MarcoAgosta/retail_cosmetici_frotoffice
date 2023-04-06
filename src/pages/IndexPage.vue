<template>
<div class="background-purple">
    <Navbar></Navbar>
    <div class="container">
        <div class v-if="noResults==true">
            <div class="row">
                <h1 class="purple col-6">Profumi in catalogo</h1>
            </div>

            <div class="row">
                <input v-model="filter" type="text" class="searchbar col-10 col-lg-6 p-2 mt-2 mb-2" placeholder="Cerca un prodotto">
                <div class="col-2 d-flex m-2 align-items-center">
                    <button @click="filterPage(filter)" class="btn btn-purple m-0">Cerca</button>
                </div>
            </div>
            <div class="d-flex justify-content-center align-items-center mt-5 pt-5 purple">
                <h3>Non ci sono risultati</h3>
            </div>
        </div>

        <div v-else-if="perfumes[0]" class="row gx-3">
            <div class="row">
                <h1 class="purple col-6">Profumi in catalogo</h1>
            </div>

            <div class="row">
                <input v-model="filter" type="text" class="searchbar col-10 col-lg-6 p-2 mt-2 mb-2" placeholder="Cerca un prodotto">
                <div class="col-2 m-2 d-flex align-items-center">
                    <button @click="filterPage(filter)" class="btn btn-purple m-0">Cerca</button>
                </div>
            </div>
            
            <div v-for="perfume in perfumes" class="col-6 col-md-4 col-xl-3 p-4 d-flex flex-column carta justify-content-between">

                <div class="d-flex justify-content-center align-items-center flex-column max-heigth">
                    <img :src="backendURL + perfume.product_img" class="mb-1 img-carta" alt="">
                </div>

                <div>
                    <h4 class="m-0 purple">{{ perfume.name }}</h4>
                    <span class="brand">{{ perfume.brand }}</span>
                </div>

            </div>
            <div class="mb-4 d-flex col-12 justify-content-end">
                <button v-if="btnPrev" @click="prevpage" class="btn btn-purple m-1">Precedente</button>
                <button v-else class="btn btn-purple m-1" disabled>Precedente</button>

                <button v-if="btnNext" @click="nextpage" class="btn btn-purple m-1">Avanti</button>
                <button v-else class="btn btn-purple m-1" disabled>Avanti</button>
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
            response:[],
            perfumes:[],
            filter:"",
            filteredPerfumes:[],
            btnNext:"",
            btnPrev:"",
            backendURL:"http://127.0.0.1:8000/storage/",
            noResults: false,
        }
    },
    components:{Navbar},
    methods:{
        fetchAllPerfumes(){
            axios.get("http://localhost:8000/api/perfumes").then((resp)=>{
                this.response=resp.data
                this.perfumes=resp.data.results.data
                this.btnNext=resp.data.results.next_page_url
                this.btnPrev=resp.data.results.prev_page_url
                })
        },
        nextpage(){
            axios.get(this.btnNext).then((resp)=>{
                this.response=resp.data
                this.perfumes=resp.data.results.data
                this.btnNext=resp.data.results.next_page_url
                this.btnPrev=resp.data.results.prev_page_url
            })
        },
        prevpage(){
            axios.get(this.btnPrev).then((resp)=>{
                this.response=resp.data
                this.perfumes=resp.data.results.data
                this.btnNext=resp.data.results.next_page_url
                this.btnPrev=resp.data.results.prev_page_url
            })
        },
        filterPage(argoument){
            this.noResults=false,
            this.perfumes=[],
            axios.get("http://localhost:8000/api/perfumes", {
                params: {
                    search: argoument
                }
            }).then((resp)=>{
                this.response=resp.data
                this.perfumes=resp.data.results.data
                this.btnNext=resp.data.results.next_page_url
                this.btnPrev=resp.data.results.prev_page_url
                if (this.perfumes.length==0){
                    this.noResults=true
                }
            })
        }
    },
    mounted(){
        this.fetchAllPerfumes()
    }
    }
</script>

<style scoped>
.max-heigth{
    max-height: 77%;
    overflow: hidden;
}
.searchbar{
    border-radius: 1rem;
    border: none;
    mask-border: none;
    border-style: none;
    margin-right: 1rem;
    margin-left: 1rem;
}
.searchbar:focus{
    outline: none;
}
.background-purple{
background-color: rgba(255, 159, 255, 0.699);
min-height: 100vh;
}
.container{
    background-color: rgb(250, 227, 230);
    padding-top: 96px;
    min-height: 100vh;
}
.carta{
    max-height: 300px;
}
.img-carta{
    max-width: 100%;
    border-radius: 5%;
    height: 100%;
    object-fit:cover;
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
.btn-purple{
    --bs-btn-color: #fff;
    --bs-btn-bg: purple;
    --bs-btn-border-color: purple;
    --bs-btn-hover-color: #fff;
    --bs-btn-hover-bg: rgb(102, 0, 102);
    --bs-btn-hover-border-color: purple;
    --bs-btn-focus-shadow-rgb: 49, 132, 253;
    --bs-btn-active-color: #fff;
    --bs-btn-active-bg: purple;
    --bs-btn-active-border-color: purple;
    --bs-btn-active-shadow: inset 0 3px 5px rgba(0, 0, 0, 0.125);
    --bs-btn-disabled-color: #fff;
    --bs-btn-disabled-bg: purple;
    --bs-btn-disabled-border-color: purple;
}
</style>