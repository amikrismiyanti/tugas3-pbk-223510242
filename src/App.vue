<script>
export default {
  data() {
    return {
      newItemText: '',
      editedItemText: '',
      items: [],
      editingIndex: -1
    }
  },
  methods: {
    addItem() {
      if (this.newItemText.trim() !== '') {
        this.items.push({ text: this.newItemText });
        this.newItemText = '';
      }
    },
    removeItem(index) {
      this.items.splice(index, 1);
      if (index === this.editingIndex) {
        this.cancelEditing();
      }
    },
    startEditing(index) {
      this.editingIndex = index;
      this.editedItemText = this.items[index].text;
    },
    cancelEditing() {
      this.editingIndex = -1;
      this.editedItemText = '';
    },
    updateItem(index) {
      if (this.editedItemText.trim() !== '') {
        this.items[index].text = this.editedItemText;
        this.cancelEditing();
      }
    }
  }
}
</script>

<template>
  <div class="todo-app">
    <h1>To Do List</h1>
    <input type="text" v-model="newItemText" @keyup.enter="addItem" placeholder="Add New Item">
    <ul class="todo-list">
      <li v-for="(item, index) in items" :key="index" class="todo-item">
        <span v-if="index !== editingIndex" class="todo-text">{{ item.text }}</span>
        <input type="text" v-model="editedItemText" v-else @keyup.enter="updateItem(index)" class="edit-input">
        <button @click="removeItem(index)" class="btn-delete">Delete</button>
        <button v-if="index !== editingIndex" @click="startEditing(index)" class="btn-edit">Edit</button>
        <button v-if="index === editingIndex" @click="cancelEditing" class="btn-cancel">Cancel</button>
      </li>
    </ul>
  </div>
</template>

<style>
.todo-app {
  max-width: 400px;
  margin: 0 auto;
  padding: 20px;
  font-family: Arial, sans-serif;
  background-color: rgb(50, 241, 210);
  border-radius: 5px;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
}

.todo-list {
  list-style-type: none;
  padding: 0;
}

.todo-item {
  margin-bottom: 10px;
}

.todo-text {
  font-size: 18px;
}

.edit-input {
  font-size: 18px;
  width: 200px;
}

.btn-delete, .btn-edit, .btn-cancel {
  background-color: #f44336;
  color: white;
  border: none;
  padding: 5px 10px;
  margin-left: 5px;
  cursor: pointer;
  border-radius: 3px;
}

.btn-edit, .btn-cancel {
  background-color: #4CAF50;
}
</style>
