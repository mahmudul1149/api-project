<template>
  <div class="edit-container">
    <div class="modalbody">
      <input type="text" v-model="editTodo.title" />
      <input type="text" v-model="editTodo.author" />
      <input type="text" v-model="editTodo.released" />
      <div class="flex">
        <button @click="saveChanges">Save Changes</button>
        <button @click="$emit('close')">Close</button>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  props: {
    editTodo: Object,
  },
  methods: {
    async saveChanges() {
      try {
        await axios.put(
          `https://backend-api-si97.onrender.com/todo/${this.editTodo.id}`,
          {
            title: this.editTodo.title,
            author: this.editTodo.author,
            released: this.editTodo.released,
          }
        );
        this.$emit("todo-updated", this.editTodo); // Emit the event with updated data
      } catch (error) {
        console.log(error);
      } finally {
        this.$emit("close");
      }
    },
  },
};
</script>

<style scoped>
.flex {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.edit-container {
  position: fixed;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
  width: 100%;
  height: 100%;
  z-index: 9999;
  background-color: rgba(0, 0, 0, 0.5);
}
.modalbody {
  width: 800px;
  padding: 2rem;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  background: white;
  z-index: 9999;
}
.modalbody input {
  display: block;
  width: 100%;
  padding: 1rem;
  margin-bottom: 1rem;
  box-sizing: border-box;
}
.cancel {
  text-align: right;
  width: 50px;
  height: 50px;
  line-height: 50px;
  text-align: center;
}
</style>
