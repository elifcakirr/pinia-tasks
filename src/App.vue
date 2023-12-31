<template>
  <main>
    <!-- heading -->
    <header>
      <img
        src="./assets/pinia-logo.svg"
        alt=""
      />

      <h1>{{ name }}</h1>
    </header>
    <div class="new-task-form">
      <TaskForm />
    </div>

    <!-- filter -->
    <nav class="filter">
      <button @click="filter = 'all'">All Tasks</button>
      <button @click="filter = 'favs'">Fav Tasks</button>
    </nav>

    <div
      class="loading"
      v-if="loading"
    >
      Loading tasks...
    </div>

    <!-- task list -->

    <div
      class="task-list"
      v-if="filter === 'all'"
    >
      <p>Your have {{ totalCount }} tasks left to do</p>
      <div v-for="task in tasks">
        <TaskDetails :task="task" />
      </div>
    </div>

    <div
      class="task-list"
      v-if="filter === 'favs'"
    >
      <p>Your have {{ favCount }} favs left to do</p>
      <div v-for="task in favs">
        <TaskDetails :task="task" />
      </div>
    </div>
  </main>
</template>

<script setup>
import { useTaskStore } from "./stores/TaskStore";
import TaskDetails from "./components/TaskDetails.vue";

import TaskForm from "./components/TaskForm.vue";
import { ref } from "vue";
import { storeToRefs } from "pinia";
const taskStore = useTaskStore();

const { tasks, loading, favs, totalCount, favCount } = storeToRefs(taskStore);

//fetch tasks
taskStore.getTasks();

const filter = ref("all");
</script>

<style scoped></style>
