<template>
<div class="container">
  <div class="row">
    <form class="col s12">
      <div class="row">
        <div class="input-field col s5">
          <i class="material-icons prefix">event_note</i>
          <textarea placeholder="Tarea" v-model="newTask.title" id="icon_prefix2" class="materialize-textarea"></textarea>
        </div>
          <div class="input-field col s2">
          <i class="material-icons prefix">query_builder</i>
          <input  type= "tel" placeholder="Tiempo estimado" v-model="newTask.time" id="icon_prefix2" class="materialize-textarea"/>
        </div>
        <div class="col s offset-s1">
          <p>total de tiempo a invertir: {{totalTime }} </p>
        </div>
      </div>
      <div class="row">
        <div class="col s12 center">
           <a class="waves-effect waves-light btn cancel" @click="addTask" >Enviar</a>
           <a class="waves-effect waves-light btn cancel" @click="cancel">Cancelar</a>
        </div>
      </div>
      <hr>
    </form>
  </div>
  <div class="row">
    <div class="col s12">
      <h3> Mi lista de tareas</h3>
      <p v-show="!tasks.length" style="color: tomato">Aun no tienes tareas pendientes</p>
    </div>
    <div v-show="tasks.length" class="col s12">
      <ol>
        <li v-for="(task ,index) in tasks">
          <p>Mi tarea: {{ task.title }}, estimo {{ task.time }} horas 
          <span @click="removeTask(index)"><i class="material-icons">delete</i> </span>
          </p>
        </li>
      </ol>
    </div>
  </div>
   <footer>@Este es mi footer!</footer>

</div> 
</template> 

<script>
export default {
  name: 'app',
  data () {
    return {
      name: 'Jonathan ',
      tasks: [],
      newTask:{
        title: '',
        time: undefined
      }
    }
  },
  created () {
    this.tasks = JSON.parse(localStorage.getItem('tasks')) || []
  }, computed: {
    totalTime () {
       if (!this.tasks.length) { 
         return 0 
       }
       let total = 0
        this.tasks.forEach(t => {
         total += parseInt(t.time)
      })
      return total
    }
  },
  methods: {
    addTask () {
      if (!this.newTask.title || !this.newTask.time) { 
        return alert('Ingresa una tarea')
      }
      this.tasks.push({
        title: this.newTask.title,
        time: this.newTask.time
      })
      localStorage.setItem("tasks", JSON.stringify(this.tasks))
      this.newTask.title = ''
      this.newTask.time = 0
    },
    removeTask (index) {
      this.tasks.splice(index, 1)
      localStorage.setItem("tasks", JSON.stringify(this.tasks))
    },
    cancel () {
      this.newTask.title = ''
      this.newTask.time = 0
    }
  }
}
</script>



<style lang="sass" scoped>
  .cancel
    background-color: black
  footer
    height: 7vh
    background: black  
    color: white
    text-align: center
</style>


