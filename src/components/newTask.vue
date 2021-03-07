<template>
  <div id="newTask" class="form-group newTask">
    <form @submit.prevent="enviarTarea" class="form"> 
      <div class="container">
        <div class="row">
          <div class="col-md-4">            
            <label>Título</label>
            <input
              ref="titulo"
              v-model="tarea.titulo"
              type="text"
              class="form-control"
              :class="{ 'is-invalid': procesando && tituloInvalido }"
              @focus="resetEstado"
              @keypress="resetEstado"
            />
          </div>
        </div>
        <div class="row">
          <div class="col-md-4">
            <label>Descripción</label>
            <textarea
              v-model="tarea.descripcion"
              type="text"
              class="descripcion"
              :class="{ 'is-invalid': procesando && descripcionInvalida }"
              @focus="resetEstado"
            />
          </div>
        </div>
        <div class="row">
          <div class="col-md-4">
            <label>Finalización</label>
            <input
                v-model="tarea.fecha"
                type="date"
                class="form-control"
                :class="{ 'is-invalid': procesando && fechaInvalida }"
                @focus="resetEstado" 
            />
          </div>
        </div>
        <div class="row">
          <div class="col-md-12">
            <div class="form-group btn-container">
              <button class="btn btn-secondary">Añadir tarea</button>
            </div>
          </div>
        </div>
      </div>

      <!--Alertas-->
      <div class="container">
        <div class="row">
          <div class="col-md-12">
            <div v-if="error && procesando" class="alert alert-danger" role="alert">
              Debes rellenar todos los campos!
            </div>
            <div v-if="correcto" class="alert alert-success" role="alert">
              La tarea ha sido agregada correctamente!
            </div>
          </div>
        </div>
      </div>
    </form>
  </div>
</template>

<script>
  export default {
    name: 'newTask',
    data() {
      return {
        procesando: false,
        correcto: false,
        error: false,

        tarea: {
          tarea: '',
          titulo: '',
          descripcion: '',
        },
      }
    },
    methods: {
      enviarTarea() {
        this.procesando = true;
        this.resetEstado();
    
        // Comprobamos la presencia de errores
        if (this.tituloInvalido || this.descripcionInvalida || this.fechaInvalida) {
          this.error = true;
          return;
        }
    
        this.$emit('add-tarea', this.tarea);
        this.$refs.titulo.focus();

        this.error = false;
        this.correcto = true;
        this.procesando = false;

        // Restablecemos el valor de la variables
        this.tarea= {
          titulo: '',
          descripcion: '',
          fecha: '',
        }
      },
      resetEstado() {
        this.correcto = false;
        this.error = false;
      },
    },
    computed: {
      tituloInvalido() {
        return this.tarea.titulo.length < 1;
      },
      descripcionInvalida() {
        return this.tarea.descripcion.length < 1;
      },
      fechaInvalida() {
        return this.tarea.fecha.length < 1;
      },
    },
  }

</script>

<style lang="scss" scoped>
.form{
  width: 100%;
  box-shadow: 0px 4px 4px rgba(0, 0, 0, 0.198);
  border-radius: 5px;
  border: 1px rgba(128, 128, 128, 0.253) solid;
  h5{
    margin: 30px;
  }
}
.row{
  margin: 15px 0px 15px 0px;
}
input:last-child{
  border-top: none;
  border-right: none;
  border-left: none;
  border-radius: 0px;
  width: 240px;
  box-shadow: none;
}
.btn-secondary{
  width: 100%;
  margin: 10px 0px 10px 0px;
  background: black;
  border-radius: 100px;
  border: none;
}
.descripcion{
  width: 240px;
  height: 100px;
  border: 1px rgba(128, 128, 128, 0.308) solid;
}
@media (max-width: 768px) {
  .col-md-4{
    margin: 15px 0px 15px 0px;
  }
}
</style>