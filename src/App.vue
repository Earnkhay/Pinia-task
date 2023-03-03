<script setup>
import {useTaskStore } from './stores/TaskStore'
import TaskDetails from './components/TaskDetails.vue'
import { ref } from 'vue';
import TaskForm from './components/TaskForm.vue';
import { storeToRefs } from 'pinia';

const store = useTaskStore()

// storetorefs hook gets all of the differenet state props and getters from the store and creates out of them
//actions cannote be used with storetorefs instead use action itself
const { tasks, loading, favs, totalCount, favCount } = storeToRefs(store)

//fetch tasks
store.getTasks()

const filter = ref('all')
</script>

<template>
  <main>
    <header>
      <img src="./assets/pinia-logo.svg" alt="pinia logo">
      <h1>Pinia Tasks</h1>
    </header>

    <div class="new-task-form">
      <TaskForm/>
    </div>

    <nav class="filter">
      <button @click="filter = 'all'">All tasks</button>
      <button @click="filter = 'favs'">Fav tasks</button>
    </nav>

    <div class="loading" v-if="loading">Loading Tasks.....</div>

    <div class="task-list" v-if="filter === 'all'">
      <p>You have {{ totalCount }} tasks left to do</p>
      <div v-for="(task, id) in tasks" :key="id">
        <TaskDetails :task="task"/>
      </div>
    </div>
    <div class="task-list" v-if="filter === 'favs'">
      <p>You have {{ favCount }} tasks left to do</p>
      <div v-for="(task, id) in favs" :key="id">
        <TaskDetails :task="task"/>
      </div>
    </div>
    
    <!-- reset the store state to the original value -->
    <button @click="store.$reset">reset</button>
  </main>
</template>
