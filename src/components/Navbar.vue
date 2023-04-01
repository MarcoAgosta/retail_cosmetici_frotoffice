<template>
<nav class="navbar navbar-light">
    <div class="container">
        <a class="navbar-brand d-flex align-items-center " href="#">
          <h3 class="d-inline-block m-0">Profumeria</h3>
          <img src="Logo-removebg-preview.png" class="d-inline-block align-top logo" alt="Logo del sito">
        </a>
    </div>
</nav>
</template>

<script>
export default{
    data(){
        return{

        }
    }
}
</script>

<style scoped>
.logo{
    width: 70px;
}
.navbar{
    position: fixed;
    right: 0;
    left: 0;
    background-color: white;
    border-bottom: 1px rgb(231, 231, 231) solid;
}

h3{
    color: purple;
}
</style>