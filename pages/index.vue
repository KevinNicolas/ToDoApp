<template>
  <div class="container">
    <Cabecera/>
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
</template>

<script>
import Cabecera from '~/components/Cabecera'
import Tareas from '~/components/Tareas'

export default {
  data () {
    return {
      pestanias: ['Tareas'],
      pestaniaActiva: 'Tareas'
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
  components: {
    Cabecera,
    Tareas
  },
  head () {
    return {
      title: 'ToDoList',
      meta: [
        // hid is used as unique identifier. Do not use `vmid` for it as it will not work
        {
          hid: 'description',
          name: 'description',
          content: 'My custom description'
        }
      ]
    }
  }
}
</script>

<style>
  .contenido{
    margin-top: 50px;
  }
  .contenido .radioButtons{
    margin-left: 20px;
  }
  .contenido .radioButtons .radioButton .el-button{
    background-color: transparent;
    border: none;
    color: #2f2d2e;
    transition: .5s ease all;
    padding: 2px;
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
    padding: 20px;
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
</style>
