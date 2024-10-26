<!-- components/HeaderComponent.vue -->
<template>
    <header class="header">
      <img :src="logoSrc" alt="Logo" class="logo" />
      <h1>Bem-vindo!</h1>
    </header>
  </template>
  
  <script>
  export default {
    name: 'HeaderComponent',
    data() {
      return {
        logoSrc: require('@/assets/logo.png') // Altere para o caminho correto da sua imagem
      };
    }
  };
  </script>
  
  <style scoped>
  .header {
    display: flex;
    align-items: center;
    padding: 5px;
    background-color: white;
    color: black;
    border: 2px solid #ddd;
    box-shadow: 5px 5px 10px rgba(0, 0, 0, 0.5);
    color: #333;
    
  }

  .header h1 {
    padding-left: 50px;
  }
  
  .logo {
    width: 120px; 
    height: auto; 
    margin-right: 1rem; 
  }
  </style>
  