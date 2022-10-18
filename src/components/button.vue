<template>
  <button
    @click="onClick"
    class="border-0 rounded-sm text-white px-3 py-2 cursor-pointer"
    :style="{ backgroundColor: color }"
  >
    {{ text }}
  </button>
</template>

<script>
export default {
  name: "ClickButton",
  props: {
    text: String,
    color: String,
  },
  emits: ["click-btn"],

  methods: {
    onClick() {
      this.$emit("click-btn");
    },
  },
};
</script>
