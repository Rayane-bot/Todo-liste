<template>
  <div id="app">
    <task v-bind:tasks="tasks"></task>
  </div>
</template>

<script>
import Task from "./components/Task";

export default {
  name: "App",
  components: {
    Task,
  },
  data() {
    return {
      tasks: [
        {
          id: 1,
          title: "Envoyer un mail",
          completed: true,
        },
        {
          id: 2,
          title: "Go Muscu",
          completed: true,
        },
        {
          id: 3,
          title: "Reviser le Vue-js",
          completed: false,
        },
        {
          id: 4,
          title: "Developper ",
          completed: false,
        },
      ],
    };
  },
};
</script>