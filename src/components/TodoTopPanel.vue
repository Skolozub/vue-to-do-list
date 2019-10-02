<template>
  <form class="form" @submit="submitForm">
    <input class="input" type="text" v-model="message">
    <button class="submit" type="submit">+ add</button>
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

<style>
.form {
  position: relative;
}

.input {
  width: 100%;
  height: 40px;
  padding: 0 85px 0 15px;
  background-color: rgba(0, 0, 0, 0.04);
  border: 0;
  transition: background-color 0.3s;
}

.input:focus {
  background-color: #FFF;
  outline: 0;
}

.submit {
  position: absolute;
  top: 0;
  right: 0;
  width: 70px;
  height: 100%;
  font-family: "Source Sans Pro", "Lucida Grande", sans-serif;
  background-color: transparent;
  border: none;
  transition: background-color 0.3s;
  cursor: pointer;
}

.submit:hover {
  background-color: #74B7709E;
}
</style>


