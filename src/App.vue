<template>
  <div id="app">
    <h1>Vue Todo List</h1>
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
      this.list = [...this.list, { id: lastElementId + 1, name: message, checked: false }];
    },
    deleteItem(itemId) {
      this.list = this.list.filter(({ id }) => id !== itemId);
    },
    toggleItemStatus(itemId) {
      this.list = this.list.reduce((acc, item) => [...acc, item.id === itemId ? {...item, checked: !item.checked} : item], []);
    }
  },
  mounted() {
    this.$root.$on("delete-item-event", this.deleteItem);
    this.$root.$on("check-item-event", this.toggleItemStatus);
  }
};
</script>

<style>
* {
  box-sizing: border-box;
}

html,
body {
  font-family: "Source Sans Pro", "Lucida Grande", sans-serif;
  line-height: 1;
}

#app {
  width: 600px;
  padding: 30px 20px;
  margin: 30px auto;
  background-color: #A5C681;
  box-shadow: 0 0 15px 0 rgba(0, 0, 0, .3);
}

</style>