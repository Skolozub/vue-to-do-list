<template>
  <li :class="{'item': true, 'item-checked': checked}">
    <div>{{name}}</div>
    <div class="btn-group">
      <button class="btn btn-delete" @click="deleteItem(id)" v-if="checked">delete</button>
      <button class="btn" @click="toggleItemStatus(id)">{{checked ? 'uncheck' : 'check'}}</button>
    </div>
  </li>
</template>

<script>
export default {
  name: "TodoItem",
  props: {
    id: Number,
    name: String,
    checked: Boolean
  },
  methods: {
    deleteItem(id) {
      this.$root.$emit("delete-item-event", id);
    },
    toggleItemStatus(id) {
      this.$root.$emit("check-item-event", id);
    }
  }
};
</script>

<style>
.item {
  position: relative;
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 8px 10px;
  margin-bottom: 5px;
  transition: background-color 0.3s;
}

.item-checked {
  text-decoration: line-through;
  color: #888;
}

.item:hover {
  background-color: rgba(0, 0, 0, 0.04);
}

.btn {
  padding: 5px 10px;
  font-family: "Source Sans Pro", "Lucida Grande", sans-serif;
  background-color: transparent;
  border: none;
  transition: background-color 0.3s;
  cursor: pointer;
}

.btn:hover {
  background-color: #74B7709E;
}

.btn-delete:hover {
  background-color: #B7A0709E;
}
</style>

