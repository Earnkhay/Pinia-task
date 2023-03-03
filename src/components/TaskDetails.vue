<script setup>
import { useTaskStore } from '../stores/TaskStore';

const props = defineProps(['task'])
const store = useTaskStore()
</script>

<template>
    <div class="task">
        <h3>{{ task.title }}</h3>
        <div class="icons">
            <i @click="store.deleteTask(task.id)"
             class="material-icons">delete</i>
            <i @click="store.toggleFav(task.id)" 
            class="material-icons"
            :class="{active: task.isFav}"
            >favorite</i>
        </div>
    </div>
</template>


<style lang="scss" scoped>

</style>