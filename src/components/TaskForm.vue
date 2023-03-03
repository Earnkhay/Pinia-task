<script setup>
import { ref } from "vue";
import { useTaskStore } from "../stores/TaskStore";

    const store = useTaskStore()
    const newTask = ref('')
    const handleSubmit = () => {
        if(newTask.value.length > 0){
            store.addTask({
                title: newTask.value,
                isFav: false,
                id: Math.floor(Math.random() * 10000) + 1
            })
            newTask.value = ''
        }
    }
</script>

<template>
    <form @submit.prevent="handleSubmit">
        <input type="text" placeholder="I need to..." v-model="newTask">
        <button>Add</button>
   </form>
</template>


<style lang="scss" scoped>

</style>