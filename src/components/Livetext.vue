<script setup>
    import { ref } from 'vue';

    const tasks = ref([
    { name: 'Task 1', time: 30 },
    { name: 'Task 2', time: 40 },
    { name: 'Task 3', time: 60 },
    { name: 'Task 4', time: 45 },
    { name: 'Task 5', time: 50 },
    ]);

    const isEditing = ref(false);
    const editedTask = ref({});

    function editTask(index) {
    editedTask.value = { ...tasks.value[index], index };
    isEditing.value = true;
    }

    function submitEdit() {
    tasks.value[editedTask.value.index] = { ...editedTask.value };

    editedTask.value = {};
    isEditing.value = false;
    }
</script>

<template>
    <!-- Popup for editing tasks -->
    <div v-if="isEditing">
        <form @submit.prevent="submitEdit">
            <label for="editName">Name:</label>
            <input v-model="editedTask.name" type="text" id="editName" required>
            
            <label for="editTime">Time:</label>
            <input v-model="editedTask.time" type="number" id="editTime" required>
    
            <button type="submit" class="mb-3">Submit</button>
        </form>
    </div>
    <div>
      <div v-for="(task, index) in tasks" :key="index" class="border p-2 mb-2">
        <p>{{ task.name }} - {{ task.time }} minutes</p>
        <button class="btn btn-success mb-3" @click="editTask(index)">Edit</button>
      </div>
    </div>
</template>
<style scoped>
    p{
        font-size: 25px;
    }
</style>
  

  