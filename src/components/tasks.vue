<template>
  <div class="tasks" :key="task.id" v-for="task in tasks">
    <Task
      @toggle-reminder="$emit('toggle-reminder', task.id)"
      @delete-task="$emit('delete-task', task.id)"
      :task="task"
    />
  </div>
</template>

<script>
import Task from "./task.vue";
export default {
  name: "MyTasks",
  emits: ["delete-task", "toggle-reminder"],
  components: { Task },
  props: {
    tasks: Array,
  },
};
</script>
