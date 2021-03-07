<template>
  <div id="board" class="board">
    <table class="table">
      <thead>
        <tr>
          <th>Título</th>
          <th>Descripción</th>
          <th>Fecha</th>
          <th></th>
        </tr>
      </thead>

      <tbody>
        <tr v-for="tarea in tareas" :key="tarea.id">
          <td v-if="editando === tarea.id">
            <input type="text" class="form-control" v-model="tarea.titulo" />
          </td>
          <td v-else>
            {{ tarea.titulo}}
          </td>
          <td v-if="editando === tarea.id">
            <input type="text" class="form-control" v-model="tarea.descripcion" />
          </td>
          <td v-else class="descripcion">
            {{ tarea.descripcion}}
          </td>
          <td v-if="editando === tarea.id">
            <input type="date" class="form-control" v-model="tarea.fecha" />
          </td>
          <td v-else>
            {{ tarea.fecha}}
          </td>
          <td v-if="editando === tarea.id">
             <i title="Guardar" class="far fa-check-circle" @click="guardar(tarea)"></i><br>
             <i title="Cancelar" class="far fa-times-circle" @click="cancelar(tarea)"></i>
          </td>
          <td v-else>
            <i title="Editar" class="far fa-edit" @click="editar(tarea)" ></i>
            <i title="Eliminar" class="far fa-trash-alt" @click="$emit('delete-tarea', tarea.id)"></i>
          </td>
        </tr>
      </tbody>
    </table>
    <div v-if="!tareas.length" class="alert alert-info" role="alert">
      No tienes tareas agregadas.
    </div>
  </div>
</template>

<script>
  export default {
    name: 'board',
    props: {
      tareas: Array,
    },
    data() {
      return {
        editando: null,
      }
    },
    methods: {
      editar(tarea) {
        this.tareaEditada = Object.assign({}, tarea);
        this.editando = tarea.id;
      },
      guardar(tarea) {
        if (!tarea.titulo.length || !tarea.descripcion.length || !tarea.fecha.length) {
          return;  
        }
        this.$emit('actualizar-tarea', tarea.id, tarea);
        this.editando = null;
      },
      cancelar(tarea) {
        Object.assign(tarea, this.tareaEditada);
        this.editando = null;
      }
    },
  }
</script>

<style lang="scss" scoped>
.board{
  width: 100%;
  box-shadow: 0px 4px 4px rgba(0, 0, 0, 0.198);
  border-radius: 5px;
  border: 1px rgba(128, 128, 128, 0.37) solid;
  padding: 10px;
  .descripcion{
    width: 380px;
  }
}
.far{
  cursor: pointer;
  margin: 0px 5px;
  font-size: 20px;
}
.fa-check-circle{
  color: green;
}
.fa-edit{
  color: orange;
}
.fa-trash-alt, .fa-times-circle{
  color: rgb(255, 0, 0);
}

</style>