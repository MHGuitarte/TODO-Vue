<template>
  <div id="todoContainer" v-on:delete="deleteTask">
    <h1 id="title">TODO List</h1>
    <div id="tasks">
      <input type="text" id="taskInput" maxlength="200" @keyup.enter="addTask()" />
      <button id="addBtn" v-on:click="addTask()">Añadir</button>
    </div>
    <TaskList v-bind:tasks="tasks" @delete="deleteTask" />
  </div>
</template>

<script>
import TaskList from "@/components/TaskList.vue";

export default {
  name: "Todo",
  components: {
    TaskList
  },
  data: function() {
    return {
      tasks: []
    };
  },
  mounted() {
    const sentences = [
      "¿Qué hacemos hoy?",
      "¡Programa una tarea!",
      "¿Algo pendiente?",
      "¡Crea una nueva tarea!"
    ];

    const counter = Math.floor(Math.random() * (sentences.length - 1));
    document.getElementById("taskInput").placeholder =
      sentences[
        counter > sentences.length - 1 ? sentences.length - 1 : counter
      ];
  },
  methods: {
    addTask: function() {
      /*Existe un pequeño error en la inclusión de nuevas tareas:
       *
       *   Al introducir una tarea y borrarla, su id se puede ver duplicada, ya
       *   que la id se genera en base a la longitud de la lista de tareas. Esto
       *   provocará que, ocasionalmente, se borren varias tareas al mismo tiempo.
       **/
      this.tasks = [
        ...this.tasks,
        {
          taskName: document.getElementById("taskInput").value,
          taskId: this.tasks.length
        }
      ];

      document.getElementById("taskInput").value = null;
    },
    deleteTask: function(idx) {
      alert(`Tarea ${this.tasks[idx].taskName} completada!`);
      this.tasks.splice(idx, 1);
    }
  }
};
</script>

<style>
#todoContainer {
  padding: 10% 30%;
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen,
    Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
}

#title {
  text-align: center;
}

#tasks {
  display: block;
  text-align: center;
}

#taskInput {
  display: inline-block;
  text-align: center;
  line-height: 30px;
  width: 70%;
  border-radius: 20px;
}

#addBtn {
  display: inline-block;
  border-radius: 15px;
  padding: 1%;
  background-color: green;
  color: white;
  font-weight: bold;
  width: 6em;
}
</style>