<template>
  <div v-show="showAddTask">
    <AddTask @add-task="add" />
  </div>

  <MyTasks
    @toggle-reminder="toggleTask"
    @delete-task="deleteTask"
    :tasks="tasks"
  />
</template>

<script>
import MyTasks from "../components/tasks.vue";
import AddTask from "../components/addTask.vue";

export default {
  name: "HomePage",
  components: {
    MyTasks,
    AddTask,
  },
  props: {
    showAddTask: Boolean,
  },
  data() {
    return {
      tasks: [],
    };
  },
  emits: ["toggle-remidner", "delete-task", "toggle-add-task", "click-btn"],

  methods: {
    async fetchTasks() {
      const res = await fetch("api/tasks");
      const data = await res.json();

      return data;
    },

    async fetchTask(id) {
      const res = await fetch(`api/tasks/${id}`);
      const data = await res.json();

      return data;
    },

    async toggleTask(id) {
      const taskToToggle = await this.fetchTask(id);
      const updateTask = { ...taskToToggle, reminder: !taskToToggle.reminder };

      const res = await fetch(`api/tasks/${id}`, {
        method: "PUT",
        headers: {
          "content-type": "application/json",
        },
        body: JSON.stringify(updateTask),
      });

      const data = await res.json();
      this.tasks = this.tasks.map((task) =>
        task.id === id ? { ...task, reminder: data.reminder } : task
      );
    },

    async add(task) {
      const res = await fetch("api/tasks", {
        method: "POST",
        headers: {
          "content-type": "application/json",
        },
        body: JSON.stringify(task),
      });

      const data = await res.json();
      this.tasks = [...this.tasks, data];
    },

    async deleteTask(id) {
      const res = await fetch(`api/tasks/${id}`, {
        method: "DELETE",
      });

      res.status === 200
        ? (this.tasks = this.tasks.filter((task) => task.id !== id))
        : alert("there is an error");
    },
  },
  async created() {
    this.tasks = await this.fetchTasks();
  },
};
</script>
