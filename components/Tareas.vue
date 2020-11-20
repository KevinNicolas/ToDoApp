<template>
    <div class="contenedor">
        <h2 class="titulo">{{tituloTarea}}</h2>
        <el-divider class="divisor" content-position="left">Crear una tarea</el-divider>
        <div class="tareasInput">
          <el-input
          class="tituloInput"
          v-model="titulo"
          placeholder="Titulo"
          clearable
          maxlength="30"
          show-word-limit>
          </el-input>
          <div @keypress.enter="agregar_tarea">
            <el-input
            class="descripsionInput"
            v-model="desc"
            placeholder="Descripsion"
            clearable
            maxlength="255"
            show-word-limit></el-input>
          </div>
          <div class="botonesInput">
            <el-button type="success" icon="el-icon-check" @click="agregar_tarea">Agregar tarea</el-button>
            <el-button type="danger" icon="el-icon-delete" @click="limpiar_inputs">Borrar tarea</el-button>
          </div>
        </div>
        <el-divider class="divisor" content-position="left">Tareas sin terminar</el-divider>
        <el-collapse v-model="collapseActivo" @change="handleChange">
          <div
          v-for="(tarea, indice) in tareas"
          :key="indice">
            <el-collapse-item v-if="!tarea[2]" :title="tarea[0]" :name="indice">
              <div>
                <h3>{{tarea[2]}}</h3>
                <p>{{tarea[1]}}</p>
                <br>
                <div class="botonesTarea">
                  <input type="checkbox" v-model="tarea[2]" :id="tarea[0]" />
                  <label :for="tarea[0]"></label>
                  <el-button type="danger" icon="el-icon-delete" circle @click="quitar_tarea(tarea[2])"></el-button>
                </div>
              </div>
            </el-collapse-item>
          </div>
          <br><br><br>
          <el-divider class="divisor" content-position="left">Tareas terminadas</el-divider>
          <div
          v-for="(tarea, indice) in tareas"
          :key="indice">
            <el-collapse-item v-if="tarea[2]" :title="tarea[0]" :name="indice">
              <div>
                <h3>{{tarea[2]}}</h3>
                <p>{{tarea[1]}}</p>
                <br>
                <div class="botonesTarea">
                  <input type="checkbox" v-model="tarea[2]" :id="tarea[0]" />
                  <label :for="tarea[0]"></label>
                  <el-button type="danger" icon="el-icon-delete" circle @click="quitar_tarea(tarea[2])"></el-button>
                </div>
              </div>
            </el-collapse-item>
          </div>
        </el-collapse>
    </div>
</template>
<script>
export default {
  data () {
    return {
      tareas: [],
      titulo: '',
      desc: '',
      checked: true
    }
  },
  props: {
    tituloTarea: {
      type: String,
      default: 'Tareas default'
    }
  },
  methods: {
    agregar_tarea (tarea) {
      if (this.titulo !== '' && this.desc !== '') {
        this.tareas.push([this.titulo, this.desc, false])
        this.limpiar_inputs()
      }
    },
    quitar_tarea (checked, indice) {
      let confirmacion = false
      if (checked) {
        confirmacion = true
      } else {
        confirmacion = confirm('¿Esta seguro que desea eliminar la tarea sin haberla terminado?')
      }
      if (confirmacion) {
        this.tareas.splice(indice, 1)
      }
    },
    limpiar_inputs () {
      this.desc = ''
      this.titulo = ''
    },
    cambiar_checkbox (checkbox) {
      this.titulo = 'holamundo'
    }
  }
}
</script>
<style scoped>
  .tareasInput{
    margin-bottom: 80px;
  }
  .tituloInput{
    width: 40%;
    height: auto;
    margin: 10px;
  }
  .botonesInput{
    float: right;
    margin: 20px 60px 0 0;
  }
  .botonesInput button:nth-child(1){
    margin-right: 20px;
  }
  .descripsionInput{
    width: 90%;
    height: auto;
    margin: 10px;
  }
  .botonesTarea button{
    margin-left: 50px;
  }
  .titulo > .el-button{
    opacity: 0;
    transition: .3s;
  }
  .titulo:hover > .el-button{
    opacity: 1;
  }
  /*estilooos*/
  input[type="checkbox"] {
    display: none;
  }
  label {
    position: relative;
  }
  label::before {
    content: "";
    background: url("https://upload.wikimedia.org/wikipedia/commons/thumb/e/e0/Check_green_icon.svg/1200px-Check_green_icon.svg.png");
    background-position: center;
    background-size: contain;
    width: 40px;
    height: 40px;
    position: absolute;
    left: -5px;
    top: -10px;
    transform: scale(0) rotateZ(180deg);
    transition: all 0.4s cubic-bezier(0.54, 0.01, 0, 1.49);
  }
  label::after {
    content: "";
    border: 2px solid #bfc0c0;
    width: 40px;
    height: 40px;
    position: absolute;
    left: -5px;
    top: -10px;
    border-radius: 50%;
  }
  input[type="checkbox"]:checked + label::before {
    transform: scale(1) rotateZ(0deg);
  }
  input[type="checkbox"]:checked + label::after {
    border: 2px solid #53c245;
  }
</style>
