<template>
  <input
    type="text"
    @input="handleInput"
    class="
      border-gray-300
      focus:border-indigo-300
      focus:ring
      focus:ring-indigo-200
      focus:ring-opacity-50
      rounded-md
      shadow-sm
    "
  />
</template>

<script>
export default {
  name: "BreezeInput",

  methods: {
    handleInput(e) {
      this.$emit("input", e.target.value);
    },
  },
};
</script>
