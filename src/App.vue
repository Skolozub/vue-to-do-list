<template>
  <div id="app">
    <h1>
      Vue Todo List
      <sup>{{itemsCount}} items, {{itemsChecked}} checked, {{itemsDeleted}} deleted</sup>
    </h1>
    <TodoTopPanel @add-to-list-event="addToList"/>
    <TodoList :list="list"/>
    <a class="link" href="https://vuejs.org/v2/guide/" target="_blank" ref="noopener noreferrer">
      <img src="./images/vue.png"> vuejs.org
    </a>
  </div>
</template>

<script>
import TodoTopPanel from "./components/TodoTopPanel";
import TodoList from "./components/TodoList";

export default {
  name: "App",
  data: () => ({
    list: [],
    itemsCount: 0,
    itemsChecked: 0,
    itemsDeleted: 0
  }),
  components: {
    TodoTopPanel,
    TodoList
  },
  methods: {
    addToList(message) {
      const { length: listLength } = this.list;
      const lastElementId = listLength ? this.list[listLength - 1].id : -1;
      this.list = [
        ...this.list,
        { id: lastElementId + 1, name: message, checked: false }
      ];
      this.itemsCount = listLength + 1;
    },
    deleteItem(itemId) {
      this.list = this.list.filter(({ id }) => id !== itemId);
      this.itemsChecked -= 1;
      this.itemsCount -= 1;
      this.itemsDeleted += 1;
    },
    toggleItemStatus(itemId) {
      this.list = this.list.reduce(
        (acc, item) => [
          ...acc,
          item.id === itemId ? { ...item, checked: !item.checked } : item
        ],
        []
      );
      this.itemsChecked = this.list.filter(({ checked }) => checked).length;
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
  min-height: 100%;
  font-family: "Source Sans Pro", "Lucida Grande", sans-serif;
  line-height: 1;
}

body {
  background: #213E31;
  background: -webkit-linear-gradient(bottom right, #213E31, #05FF9E);
  background: -moz-linear-gradient(bottom right, #213E31, #05FF9E);
  background: linear-gradient(to top left, #213E31, #05FF9E);
}

sup {
  padding-left: 10px;
  color: #8e8e8e;
}

#app {
  position: relative;
  width: 600px;
  padding: 30px 20px;
  margin: 30px auto;
  background-color: #A5C681;
  box-shadow: 0 0 15px 0 rgba(0, 0, 0, 0.3);
}

.link {
  position: absolute;
  bottom: 10px;
  right: 10px;
  display: flex;
  align-items: center;
  color: #000;
}

.link img {
  width: 30px;
  height: auto;
}
</style>