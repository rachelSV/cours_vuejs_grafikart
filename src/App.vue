<!-- HTML -->
<template>
  <!-- 2 -->
  <form action="" @submit.prevent="addTodo"> <!-- Déclare un formulaire qui appelle la méthode addTodo sans recharger la page lorsque soumis -->
    <p>Créer une nouvelle tâche :</p>
    <input type="text" placeholder="Tâche à effectuer" v-model="newTodo"> <!--v-model pour récupérer / lier la valeure du champs de l'input à newTodo-->
    <button>Ajouter</button>
    <div v-if="todos.length == 0">Vous n'avez pas de tâches à faire</div> <!-- S'il n'y a pas de tâches, afficher ce message-->
    <div v-else> <!-- si des tâches existent : -->
      <ul>
        <li v-for="todo in sortedTodos()" :key="todo.date" :class="{completed: todo.completed}"><!-- boucle qui parcourt les tâches triées et applique une class pour barrer les tâches en css au coche-->
          <label>
            <input type="checkbox" v-model="todo.completed"> <!-- quand on coche la checkbox, completed passe à true, et en décochant completed passe à false-->
            {{ todo.title }} <!-- affiche le titre de la tâche dans la liste ...-->
          </label>
        </li>
      </ul>
    </div>
  </form>
</template>



<!-- JAVASCRIPT -->
<script setup>

import {ref} from 'vue'
//tâche de test par défaut 
const todos = ref([{
  title: 'tâche de test',
  completed: true,
  date: 1,
}])

// Initialise une variable réactive pour contenir la tâche entrée par l'utilisateur
const newTodo = ref('')
// Fonction pour ajouter une nouvelle tâche à la liste et vider l'input après soumission.
const addTodo = ( )=> {
  todos.value.push({
    title: newTodo.value,
    completed: false,
    date: Date.now()
  })
  newTodo.value = '' // Vide l'input quand je soumet le formulaire
}
// fonction sortedTodos permet de mettre les nouvelles tâches en 1ère position puis une fois cochées de les foutre en bas
const sortedTodos = () => {
  return todos.value.toSorted((a, b) => a.completed > b.completed ? 1 : -1) // Trie les tâches en fonction de leur état completed
}
</script>



<!-- CSS -->
<style>
.completed {
  opacity : 50%;
  text-decoration: line-through;
}
</style>