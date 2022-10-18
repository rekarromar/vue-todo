<template>
  <div
    @dblclick="$emit('toggle-reminder', this.id)"
    :class="[
      task.reminder == 1 ? 'border-l-4 border-black' : '',
      'flex justify-between items-center p-1 mb-3 ',
    ]"
  >
    <h3>{{ task.task }}</h3>
    <button
      @click="$emit('delete-task', id)"
      class="text-white px-3 py-2 bg-black rounded-sm cursor-pointer hover:bg-red-700"
    >
      Delete
    </button>
  </div>
</template>

<script>
export default {
  name: "OneTask",
  emits: ["toggle-remidner", "delete-task"],
  props: {
    task: Object,
  },
};
</script>

<style scoped>
.btn:hover {
  background: rgb(40, 38, 38);
  cursor: pointer;
}
.task {
  /* display: flex;
  justify-content: space-between;
  align-items: center;
  background-color: white;
  margin-bottom: 10px;
  border-radius: 2px;
  padding: 5px; */
}

.reminder {
  /* border-left: 5px solid black; */
}
</style>
