<template>
  <div id="app" class="appContainer">
    <header>
      <headerLolweb/>
    </header>
    <main>
      <board
        :tareas="tareas"
        @delete-tarea="eliminarTarea"
        @actualizar-tarea="actualizarTarea"
      />
      <newTask @add-tarea="agregarTarea"/>
    </main>
    <footer>
      <footerLolweb/>
    </footer>
  </div>
</template>

<script>
import newTask from './components/newTask.vue'
import board from './components/board.vue'
import headerLolweb from './components/header.vue'
import footerLolweb from './components/footer.vue'

export default {
  name:'app',
  components: {
    headerLolweb,
    newTask,
    board,
    footerLolweb,
  },
  data() {
    return {
      tareas: [    
      ],
    }
  },
  methods: {
    agregarTarea(tarea) {
      let id = 0;
    
      if (this.tareas.length > 0) {
        id = this.tareas[this.tareas.length - 1].id + 1;
      }
    
      this.tareas= [...this.tareas, { ...tarea, id}];
    },

    eliminarTarea(id) {
      this.tareas = this.tareas.filter(
      tarea => tarea.id !== id
      );
    },

    actualizarTarea(id, tareaActualizada) {
      this.tareas = this.tareas.map(tarea =>
      tarea.id === id ? tareaActualizada : tarea)
    }
  },
}
</script>

<style lang="scss">
*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
main{
  width: 100%;
  display: grid;
  grid-template-columns: 1fr 300px;
  grid-gap: 15px;
  white-space: 20px;
  padding: 20px;
}
board{
  grid-column: 1/2;
}
newTask{
  grid-column: 2/3;
}
</style> >
