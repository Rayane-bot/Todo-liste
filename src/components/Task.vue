<template>
  <div class="container">
    <div class="task">
      <!-- title -->
      <div class="title">
        <h1> Todo Liste</h1>
      </div>
      <!-- form -->
      <div class="form">
        <input
          type="text"
          placeholder="Nouvelle Liste"
          v-model="newTask"
          @keyup.enter="addTask"
        />
        <button @click="addTask"><i class="fas fa-plus"></i></button>
      </div>
      <!-- listes -->
      <div class="taskItems">
        <ul>
          <task-item
            v-bind:task="task"
            v-for="(task, index) in tasks"
            :key="task.id"
            @remove="removeTask(index)"
            @complete="completeTask(task)"
          ></task-item>
        </ul>
      </div>
      <!-- buttons -->
      <div class="clearBtns">
        <button @click="clearCompleted">Actualiser la liste !</button>
        <button @click="clearAll">Retirer tout !</button>
      </div>
      <!-- pending -->
      <div class="pendingTasks">
        <span>Listes restante: {{ incomplete }}</span>
      </div>
    </div>
  </div>
</template>

<script>
import TaskItem from "./Task-item";

export default {
  name: "Task",
  props: ['tasks'],
  components: {
    TaskItem,
  },
  data() {
    return {
      newTask: "",
    };
  },
  computed: {
    incomplete() {
      return this.tasks.filter(this.inProgress).length;
    },
  },
  methods: {
    addTask() {
      if (this.newTask) {
        this.tasks.push({
          title: this.newTask,
          completed: false,
        });
        this.newTask = "";
      }
    },
    inProgress(task) {
      return !this.isCompleted(task);
    },
    isCompleted(task) {
      return task.completed;
    },
    clearCompleted() {
      this.tasks = this.tasks.filter(this.inProgress);
    },
    clearAll() {
      this.tasks = [];
    },
    completeTask(task) {
      task.completed = !task.completed;
    },
    removeTask(index) {
      this.tasks.splice(index, 1);
    },
  },
};
</script>
