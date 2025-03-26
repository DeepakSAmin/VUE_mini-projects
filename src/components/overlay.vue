<template>
    <div v-if="show" class="overlay">
      <div class="modal">
        <slot></slot> 
        <button @click="$emit('close')" class="close">CLOSE</button>
      </div>
    </div>
  </template>
  
  <script setup>
  defineProps({
    show: Boolean, 
  });
  </script>
  
  <style scoped>
  .overlay {
    position: fixed;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.77);
    z-index: 10;
    display: flex;
    align-items: center;
    justify-content: center;
  }
  
  .modal {
    width: 750px;
    background-color: white;
    border-radius: 10px;
    padding: 30px;
    position: relative;
    display: flex;
    flex-direction: column;
  }
  
  .close {
    background-color: #b11a21;
    color: white;
    padding: 10px;
    border: none;
    margin-top: 10px;
    cursor: pointer;
  }
  </style>
  