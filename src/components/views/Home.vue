<template>
  <AddTask v-show="showAddTaskForm" @add-task="addTask" />
  <Tasks
    @delete-task="deleteTask"
    @toggle-reminder="toggleReminder"
    :tasks="tasks"
  />
  <Footer />
</template>

<script>
import AddTask from "../AddTask";
import Tasks from "../Tasks";
import Footer from "../Footer";

export default {
  name: "Home",
  components: {
    Tasks,
    AddTask,
    Footer,
  },
  props: {
    showAddTaskForm: Boolean,
  },
  data() {
    return {
      tasks: [],
    };
  },
  methods: {
    async addTask(task) {
      const data = await fetch("/api/tasks", {
        method: "POST",
        headers: {
          "Content-type": "application/json",
        },
        body: JSON.stringify(task),
      }).then((res) => res.json());

      this.tasks = [...this.tasks, data];
    },
    deleteTask(id) {
      if (confirm("Are you sure?")) {
        fetch(`/api/tasks/${id}`, {
          method: "DELETE",
        }).then(() => {
          this.tasks = this.tasks.filter((task) => task.id !== id);
        });
      }
    },
    async fetchTasks() {
      const data = await fetch("/api/tasks").then((response) =>
        response.json()
      );
      return data;
    },
    async toggleReminder(id) {
      const task = await fetch(`/api/tasks/${id}`).then((res) => res.json());
      const updatedTask = { ...task, reminder: !task.reminder };

      fetch(`/api/tasks/${id}`, {
        method: "PUT",
        headers: {
          "Content-type": "application/json",
        },
        body: JSON.stringify(updatedTask),
      }).then(() => {
        const tasks = [...this.tasks];

        this.tasks = tasks.map((task) =>
          task.id === id ? { ...task, reminder: !task.reminder } : task
        );
      });
    },
  },
  async created() {
    this.tasks = await this.fetchTasks();
  },
};
</script>