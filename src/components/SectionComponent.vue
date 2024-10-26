<!-- components/SectionComponent.vue -->
<template>
    <section class="section">
        <CalculadoraComponent />
    </section>
  </template>
  
  <script>
    import CalculadoraComponent from './CalculadoraComponent.vue';

    export default {
     name: 'SectionComponent',
        components: {
            CalculadoraComponent 
        }
    };
  </script>
  
  <style scoped>
  .section {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    padding: 2rem;
    background-color: #f9f9f9; 
    border: 1px solid #ddd; 
    box-shadow: 5px 5px 10px rgba(0, 0, 0, 0.5);
    margin-top: 1rem;
  }
  h2 {
    color: #333; 
  }
  p {
    color: #666; 
  }
  </style>
  