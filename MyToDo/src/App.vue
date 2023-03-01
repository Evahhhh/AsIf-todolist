<template>
  <div>
    <h1>Ma To-Do List</h1>
    <ul>
      <li v-for="(task, index) in tasks" :key="index">{{ task }}</li>
    </ul>
    <form @submit.prevent="addTask">
      <input type="text" v-model="newTask" name="newTask" placeholder="Ajouter une tâche" />
      <button type="submit">Ajouter</button>
  </form>

  </div>
</template>

<script>
import { reactive, onMounted } from "vue";

export default {
  setup() {
    const state = reactive({
      tasks: [],
      newTask: "",
    });

    // Charger les données depuis le local storage lorsque le composant est monté
    onMounted(() => {
      console.log("Le composant est monté");
      const savedTasks = localStorage.getItem("tasks");
      console.log("Les tâches enregistrées sont : ", savedTasks);
      if (savedTasks) {
        state.tasks = JSON.parse(savedTasks);
      }
    });

    const addTask = () => {
      if (state.newTask !== "") {
        state.tasks.push(state.newTask);
        state.newTask = "";
        // Enregistrer les données dans le local storage après l'ajout d'une tâche
        localStorage.setItem("tasks", JSON.stringify(state.tasks));
        console.log("Les tâches enregistrées sont : ", localStorage.getItem("tasks"));
      }
    };

    console.log("Les tâches initialisées sont : ", state.tasks);

    return {
      tasks: state.tasks,
      newTask: state.newTask,
      addTask,
    };
  },
};


</script>
