<template>
  <body class="d-flex flex-column">
 
  <footer id="sticky-footer" class="flex-shrink-0 py-4 bg-light text-white-50">
    <div class="container text-center">
      <small>Copyright &copy; tayLewis 2022</small>
    </div>
  </footer>
</body>
</template>

<script>
export default {

}
</script>

<style scoped>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#page-content {
  flex: 1 0 auto;
}

/* Other Classes for Page Styling */


.container {
  color: white;
  background-image: linear-gradient(260deg, #e20e0e 0%, #5c0a6b 100%);
  height: 40px;
  text-align: center;
  padding: 10px;
}
footer {
  z-index: 1000;
  position: fixed;
  bottom: 0;
  left: 0;
  width: 100%;
}
</style>