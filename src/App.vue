<template>
  <div id="app">
    <TodoTopPanel @add-to-list-event="addToList"/>
    <TodoList :list="list"/>
  </div>
</template>

<script>
import TodoTopPanel from "./components/TodoTopPanel";
import TodoList from "./components/TodoList";

export default {
  name: "App",
  data: () => ({
    list: []
  }),
  components: {
    TodoTopPanel,
    TodoList
  },
  methods: {
    addToList(message) {
      const { length: listLength } = this.list;
      const lastElementId = listLength ? this.list[listLength - 1].id : -1;
      this.list = [...this.list, { id: lastElementId + 1, name: message }];
    },
    deleteItem(deleteId) {
      this.list = this.list.filter(({ id }) => id !== deleteId);
    }
  },
  mounted() {
    this.$root.$on("delete-item-event", this.deleteItem);
  }
};
</script>