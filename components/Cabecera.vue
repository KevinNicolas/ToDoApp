<template>
    <div class="cabecera">
        <img class="logo" src="../static/svg/logo.svg" alt="Logo">
        <h1 class="titulo">ToDoList</h1>
        <div class="usuario">
            <el-button class="botonUsuario" type="text">Ingresar</el-button>
            <el-button class="botonUsuario" type="text">Registrarse</el-button>
        </div>
    </div>
</template>

<script>
export default {
}
</script>

<style scoped>
    .cabecera{
        background-color: #13293d;
        padding: 10px 50px;
        display: flex;
        flex-flow: row wrap;
        align-content: center;
        align-items: center;
    }
    .logo{
        width: 5%;
        min-width: 50px;
        height: auto;
    }
    .titulo{
        color: #2970ca;
        box-sizing: border-box;
        margin-left: 10px;
        width: 70%;
        font-size: 28px;
    }
    .usuario .botonUsuario:nth-child(2){
        margin-left: 20px;
    }
    @media screen and (max-width: 850px){
        .titulo{
            width: 60%;
        }
    }
    @media screen and (max-width: 650px){
        .titulo{
            width: 50%;
        }
    }
</style>
