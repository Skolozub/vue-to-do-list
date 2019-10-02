<template>
  <div>
    <ul class="list">
      <TodoItem :id="item.id" :name="item.name" v-for="item in list" v-bind:key="item.id"/>
    </ul>
    <pre>{{list}}</pre>
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

<style>
.list {
  padding-left: 0;
  margin: 20px 0;
  list-style-type: none;
}
</style>