<script setup>
import { ref } from "vue";

import { useTaskStore } from "@/store/Task";

import InputBar from "./InputBar.vue";

const taskStore = useTaskStore();
const taskTitle = ref("");

const handleAddTask = async () => {
  const title = taskTitle.value.trim();
  if (title) {
    const newTask = {
      title,
      completed: false,
    };
    await taskStore.addTask(newTask);
    taskTitle.value = "";
  }
};
</script>

<template>
  <div class="add-task-container">
    <input-bar
      placeholder="New Todo"
      v-model="taskTitle"
      @keyup.enter="handleAddTask"
    />
    <button
      class="add-task"
      :disabled="taskStore.isLoading"
      @click="handleAddTask"
    >
      Add
    </button>
  </div>
</template>

<style>
.add-task-container {
  display: flex;
  gap: 5px;
  width: 100%;
}
.add-task {
  background-color: #317ed6;
  padding: 8px;
  border-radius: 6px;
  margin: 10px 0;
  color: #fff;
}
</style>
