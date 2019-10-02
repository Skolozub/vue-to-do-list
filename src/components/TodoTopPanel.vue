<template>
  <div>
    <input type="text" v-model="message">
    <button @click="add">+ add</button>
  </div>
</template>

<script>
export default {
  name: "TodoTopPanel",
  data: () => ({
    message: ""
  }),
  methods: {
    add() {
      this.$emit("add-to-list-event", this.message);
      this.message = "";
    }
  }
};
</script>

