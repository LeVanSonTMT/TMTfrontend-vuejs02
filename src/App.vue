<template>
  <div id="app">
    <router-view>
      <template v-slot:LayoutContent>
        <router-view name='content'/>
      </template>
    </router-view>
  </div>
</template>

<script>  


export default {
  name: 'App',

  
   methods: {
    
  }
}
</script>

<style src="../public/AdminLTE-3.0.5/dist/css/adminlte.min.css"></style>

<style src="../plugins/tempusdominus-bootstrap-4/css/tempusdominus-bootstrap-4.min.css"></style>
<style src="../plugins/icheck-bootstrap/icheck-bootstrap.min.css"></style>
<style src="../plugins/overlayScrollbars/css/OverlayScrollbars.min.css"></style>
<style src="../plugins/daterangepicker/daterangepicker.css"></style>
<style src="../plugins/summernote/summernote-bs4.css"></style>


<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  background-color: #e9ecef;
  
}
html, 
body {
    margin: 0;
    padding: 0;
    background-color: #e9ecef;
}
</style>
