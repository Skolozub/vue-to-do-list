<template>
  <div>
    <ul v-for="item in list" v-bind:key="item.id">
      <TodoItem :id="item.id" :name="item.name"/>
    </ul>
    {{list}}
  </div>
</template>

<script>
import TodoItem from "./TodoItem";
export default {
  name: "TodoList",
  components: { TodoItem },
  props: {
    list: Array
  }
};
</script>

