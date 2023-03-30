<template>
<h1>Pagina index</h1>
</template>

<script>
import { reactive } from "vue";
import axios from "axios";
export default{
    data(){
        return{
            perfumes:[]
        }
    },
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