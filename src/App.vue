<!-- App.vue -->
<template>
  <div id="app">
    <HeaderComponent />
    <SectionComponent />
  </div>
</template>

<script>
import HeaderComponent from './components/HeaderComponent.vue';
import SectionComponent from './components/SectionComponent.vue';

export default {
  name: 'App',
  components: {
    HeaderComponent,
    SectionComponent
  }
};
</script>

<style>

#app {
  display: flex;
  flex-direction: column;
  font-family: Avenir, Helvetica, Arial, sans-serif; 
  -webkit-font-smoothing: antialiased; 
  -moz-osx-font-smoothing: grayscale; 
  text-align: center; 
  color: #2c3e50; 
  margin: 20px; 
}
</style>

