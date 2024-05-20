<template>
    <div class="child-container">
      <button @click="sendData">Send</button>
    </div>
  </template>
  
  <script setup>
  import { defineEmits } from 'vue';
  const emit = defineEmits(['send']);
  
  const sendData = () => {
    emit('send', 'Data dari Child Component');
  };
  </script>
  
  <style scoped>
  .child-container {
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 20px;
  }
  
  button {
    padding: 10px 20px;
    font-size: 16px;
    color: white;
    background-color: rgb(0, 130, 139);
    border: none;
    border-radius: 5px;
    cursor: pointer;
    transition: background-color 0.3s ease, transform 0.2s ease;
  }
  
  button:hover {
    background-color: rgb(0, 130, 139);
    transform: scale(1.05);
  }
  
  button:active {
    transform: scale(0.95);
  }
  </style>
  