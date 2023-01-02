<template>
  <div id="app">
    <HeaderGDE></HeaderGDE>
    <!-- filtros y cuadricula principal -->
    <MainGDE></MainGDE>
  </div>
</template>

    <script>

    import HeaderGDE from './components/HeaderGDE.vue'
    import MainGDE from './components/mainGDE/MainGDE.vue'

    export default {
      name: 'app',
      components: {
        HeaderGDE,
        MainGDE,
        
      }
    }
    </script>

<style>
* {
    margin: 0;
    padding: 0;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  
}
</style>
