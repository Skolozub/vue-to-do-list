<template>
  <form @submit="submitForm">
    <input type="text" v-model="message">
    <button type="submit">+ add</button>
  </form>
</template>

<script>
export default {
  name: "TodoTopPanel",
  data: () => ({
    message: ""
  }),
  methods: {
    submitForm(event) {
      event.preventDefault();

      const emptyInputString = !this.message;
      if (emptyInputString) return null;

      this.$emit("add-to-list-event", this.message);
      this.message = "";
    }
  }
};
</script>

