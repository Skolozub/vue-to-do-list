<template>
  <div>
    <div>{{name}}</div>
    <button @click="deleteItem(id)">delete</button>
    <button>checked</button>
  </div>
</template>

<script>
export default {
  name: "TodoItem",
  props: {
    name: String,
    id: Number
  },
  methods: {
    deleteItem(id) {
      this.$root.$emit("delete-item-event", id);
    }
  }
};
</script>
