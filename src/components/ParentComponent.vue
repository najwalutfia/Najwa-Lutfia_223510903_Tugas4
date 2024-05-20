<template>
    <div class="parent-container">
      <h3>Parent Component</h3>
      <ChildComponent @send="addItem" />
      <NestedChildComponent>
        <template v-if="items.length">
          <ul>
            <li v-for="(item, index) in items" :key="index">
              <span v-if="!isEditing[index]">{{ item }}</span>
              <input v-if="isEditing[index]" v-model="items[index]" />
              <button @click="editItem(index)">{{ isEditing[index] ? 'Simpan' : 'Edit' }}</button>
              <button @click="deleteItem(index)">Hapus</button>
            </li>
          </ul>
        </template>
        <p v-else>Tidak ada item.</p>
      </NestedChildComponent>
      <p class="received-data">{{ receivedData }}</p>
    </div>
  </template>
  
  <script setup>
  import { ref } from 'vue';
  import ChildComponent from './ChildComponent.vue';
  import NestedChildComponent from './NestedChildComponent.vue';
  
  const items = ref([]);
  const isEditing = ref([]);
  const receivedData = ref('');
  
  const addItem = (data) => {
    if (data.trim() !== '') {
      items.value.push(data);
      isEditing.value.push(false);
    }
  };
  
  const editItem = (index) => {
    isEditing.value[index] = !isEditing.value[index];
  };
  
  const deleteItem = (index) => {
    items.value.splice(index, 1);
    isEditing.value.splice(index, 1);
  };
  
  const displayData = (data) => {
    receivedData.value = data;
  };
  </script>
  
  <style scoped>
  .parent-container {
    border: 2px solid #975b5b;
    padding: 20px;
    border-radius: 10px;
    max-width: 600px;
    margin: 20px auto;
    box-shadow: 0 4px 8px rgba(233, 230, 230, 0.993);
  }
  
  h3 {
    color: #200c0c;
    text-align: center;
  }
  
  .received-data {
    margin-top: 20px;
    padding: 10px;
    background-color: #e98b8b;
    border: 1px solid #0c0202;
    border-radius: 5px;
  }
  
  ul {
    list-style-type: none;
    padding: 0;
  }
  
  li {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 10px;
    border: 1px solid #0e0606;
    border-radius: 5px;
    margin-bottom: 10px;
    background-color: #fca0a0;
  }
  
  li input {
    flex: 1;
    padding: 5px;
    font-size: 16px;
    margin-right: 10px;
  }
  
  button {
    padding: 10px 20px;
    font-size: 16px;
    color: rgb(243, 241, 241);
    background-color: rgb(0, 183, 255);
    border: none;
    border-radius: 5px;
    cursor: pointer;
    transition: background-color 0.3s ease;
  }
  
  button:hover {
    background-color: rgb(49, 201, 221);
  }
  
  li button {
    margin-left: 10px;
  }
  </style>
  