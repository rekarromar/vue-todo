<template>
  <header class="flex justify-between items-center mb-4">
    <h1 class="text-4xl text-red-700 text-center">Task Tracker</h1>
    <ClickButton
      v-show="homePage"
      @click-btn="$emit('toggle-add-task')"
      :text="showAddTask ? 'close' : 'Add Task'"
      :color="showAddTask ? 'red' : 'black'"
    />
  </header>
</template>

<script>
import ClickButton from "./button.vue";
export default {
  name: "HeaderSection",
  emits: ["toggle-add-task"],
  props: {
    showAddTask: Boolean,
  },
  components: { ClickButton },
  computed: {
    homePage() {
      if (this.$route.path == "/") {
        return true;
      } else {
        return false;
      }
    },
  },
};
</script>
