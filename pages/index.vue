<template>
  <div class="container">
    <div>
      <Cabecera />
      <div class="contenido">
        <div class="radioButtons">
          <el-radio-group v-model="pestaniaActiva">
            <el-radio-button
            class="radioButton"
            v-for="(pestania, indice) in pestanias"
            :key="indice"
            :label="pestania">
            {{pestania}}
            <el-button
            icon="el-icon-close"
            circle
            @click="quitar_categoria(pestania, indice)"></el-button>
            </el-radio-button>
            <el-button icon="el-icon-plus" @click="agregar_categoria"></el-button>
          </el-radio-group>
        </div>
        <div class="tareas">
          <div>
            <Tareas
            v-for="(pestania, indice) in pestanias"
            :key="indice"
            :tituloTarea="pestania"
            v-show="pestania == pestaniaActiva"/>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Cabecera from '~/components/Cabecera'
import Tareas from '~/components/Tareas'

window.addEventListener('hashchange', () => {
  switch (window.location.hash) {
    case '#/ingresar': alert(this.modo + ' ' + this.mostrar_usuario); break
    default: this.ingresar(); break
  }
})

export default {
  data () {
    return {
      pestanias: ['Tareas'],
      pestaniaActiva: 'Tareas',
      mostrar_usuario: false,
      modo: 'register'
    }
  },
  methods: {
    agregar_categoria () {
      const nombre = prompt('Ingresar el nombre de la categoria')
      let valido = true
      this.pestanias.forEach((element) => {
        if (element === nombre) {
          valido = false
        }
      })
      if (valido) {
        this.pestanias.push(nombre)
      } else {
        alert('El nombre "' + nombre + '" ya existe')
      }
    },
    quitar_categoria (categoria, indice) {
      const quitarCategoria = confirm('¿Seguro que desea eliminar la categoria ' + categoria + '?')
      if (quitarCategoria) {
        this.pestanias.splice(indice, 1)
      }
    }
  },
  fetch () {
    window.addEventListener('hashchange', () => {
      switch (window.location.hash) {
        case '#/ingresar': this.modo = 'login'; this.mostrar_usuario = true; break
        case '#/registrarse': this.modo = 'register'; this.mostrar_usuario = true; break
        default: this.mostrar_usuario = false
      }
    })
  },
  components: {
    Cabecera,
    Tareas
  }
}
</script>

<style>
  .contenido{
    margin: 50px 0;
  }
  .contenido .radioButtons{
    margin-left: 20px;
  }
  .contenido .radioButtons .radioButton .el-button{
    background-color: transparent;
    border: none;
    color: #2f2d2e;
    transition: .5s ease all;
    padding: 0px 0;
    margin: 1.5px 1px;
  }
  .contenido .radioButtons .radioButton.is-active .el-button{
    color: white;
  }
  .contenido .radioButtons .radioButton .el-button:hover{
    color: #dd2698;
  }
  .tareas{
    min-width: 100px;
    min-height: 100px;
    background-color: #2f2d2e;
    padding: 40px 20px;
    color: #e8f1f2;
  }
  .el-divider__text{
    background-color: #2f2d2e;
    color: #e8f1f2;
  }
  .el-collapse-item__header, .el-collapse-item__content{
    padding: 10px;
    background-color: #2f2d2e;
    color: #e8f1f2;
  }
  .el-collapse-item__content{
    padding-left: 20px;
  }
  .el-collapse-item__header{
    color: #2970ca;
    font-weight: bolder;
    font-size: 16px;
    transition: .5s ease color;
    padding: 0 20px;
  }
  .el-collapse-item__header:hover{
    color: #4a83ce;
  }
  .el-collapse-item__header i{
    color: white;
  }
  @media screen and (max-width: 400px){
    .tareas{
      padding: 10px;
    }
  }
</style>
