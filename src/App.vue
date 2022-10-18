<template>
  <div class="box-border h-full m-auto p-20">
    <div
      class="max-w-lg antialiased m-auto border-2 border-black rounded-sm p-5"
    >
      <Header :showAddTask="showAddTask" @toggle-add-task="toggleAddTask" />

      <router-view :showAddTask="showAddTask"></router-view>

      <Footer />
    </div>
  </div>
</template>

<script>
import Header from "./components/header.vue";
import Footer from "./components/footer.vue";

export default {
  name: "App",
  components: { Header, Footer },

  data() {
    return {
      showAddTask: false,
    };
  },

  methods: {
    toggleAddTask() {
      this.showAddTask = !this.showAddTask;
    },
  },
};
</script>
