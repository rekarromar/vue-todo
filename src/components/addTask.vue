<template>
  <form @submit="onSubmit" class="mb-4">
    <div class="mb-5">
      <label class="block">Task</label>
      <input class="w-full border-2 p-1" v-model="task" type="text" />
    </div>

    <div class="mb-5">
      <label>Date & Time</label>
      <input class="w-full border-2 p-1" v-model="date" type="datetime" />
    </div>

    <div class="flex justify-between items-center mb-5">
      <label class="flex-1">Set reminder</label>
      <input class="flex-2" v-model="reminder" type="checkbox" />
    </div>

    <input
      type="submit"
      class="w-full bg-black p-2 text-white"
      value="Add Task"
    />
  </form>
</template>

<script>
export default {
  name: "AddTask",
  emits: ["add-task"],
  data() {
    return {
      task: "",
      date: "",
      reminder: false,
    };
  },
  methods: {
    onSubmit(e) {
      e.preventDefault();
      console.log(1);

      if (!this.task) {
        alert("please add a task");
        return;
      }

      const newTask = {
        // id: Math.floor(Math.random() * 100000),
        task: this.task,
        date: this.date,
        reminder: this.reminder,
      };

      console.log(newTask);

      this.$emit("add-task", newTask);

      this.task = "";
      this.date = "";
      this.reminder = "";
    },
  },
};
</script>

<style scoped>
.form-section input {
  width: 100%;
  height: 30px;
}

.form-section-check {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.form-section-check label {
  flex: 1;
}

.form-section-check input {
  height: 20px;
  flex: 2;
}

.add-task {
  background: black;
  color: white;
  text-align: center;
  padding: 10px;
  width: 100%;
}

.add-task:hover {
  background: rgb(40, 38, 38);
  cursor: pointer;
}
</style>
