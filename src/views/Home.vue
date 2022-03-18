<template>
<div class= 'container'>
<div class="container_content">
<div class="container_content_inner">
<div class="title">
  <h1>Welcome to tayLewis</h1>
</div>
<div class="par">
<p>
This is a blogging site where you can find and post blogs about the 2 GREATEST people on earth: Lewis Hamilton and Taylor Swift.
</p>
</div>
<div class="btns">
    <router-link :to="{ name: 'Login' }"><button class='btnsmore active'>Login</button></router-link>
    <router-link :to="{ name: 'Register' }"><button class='btnsmore active'>Register </button></router-link>

</div>
</div>
</div>
 <div class="container_outer_img">
 <div class="img-inner">
 <img src='https://i.postimg.cc/cJzB57ST/taylorandlewisblogbackground-1.jpg'  alt="" class="container_img"/>
       </div>
     </div>
  </div>
<div class="overlay"></div>
</template>

<script>


export default {

}
</script>
<style scoped>

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

:root {
  --secondary-color: #151226;
  --contrast-color: #BF307F;
}
.overlay {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  height: 100%;
  z-index: -10;
  background-color: #8500e4;
}

.container {
  display: flex;
  height: 100vh;
  justify-content: space-around;
  align-items: center;
  color: #fff;
  animation: expand .8s ease forwards;
  background-color: var(--secondary-color);
  position: relative;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
  transition: all .8s ease;
    --secondary-color: #20e6b3;
  --contrast-color: #8500e4;
}

.container_content {
 width: 50%;
}

.container_content_inner {
  width: 80%;
  margin-left: 80px;
}

.container_outer_img {
  margin: 50px;
  width: 50%;
  overflow: hidden;
}   
    
.container_img {
  width: 100%;
  animation: slideIn 1.5s ease-in-out forwards;
}

.par {
  height: auto;
  overflow: hidden;
}

p{
  line-height: 28px;
  transform: translateY(300px);
  animation: slideUp .8s ease-in-out forwards .8s;
}

.btns {
  height: 100%;
  position: relative;
  width: 150px;
  overflow: hidden;
}

.btnsmore {
  background: transparent;
  border: 1px solid var(--contrast-color);
  border-radius: 50px;
  padding: 8px 12px;
  color: #8500e4;
  font-size: 16px;
  text-transform: uppercase;
  position: relative;
  margin-top: 15px;
  outline: none;
  transform: translateY(50px);
  animation: slideUp .8s ease-in-out  forwards 1s;
  align-content: center;
}

.active, .btnsmore:hover {
  background-color: #8500e4;
  color: white;
}

.title {
  overflow: hidden;
  height: auto;
}

h1 {
    font-size: 40px;
    color: var(--contrast-color);
    margin-bottom: 20px;
    transform: translateY(100px);
    animation: slideUp .8s ease forwards .5s;
}

@keyframes slideIn {
  0% {
    transform: translateX(500px) scale(.2);
  }
  100% {
    transform: translateX(0px) scale(1);
  }
}

@keyframes slideUp {
  0% {
    transform: translateY(300px);
  }
  100% {
    transform: translateY(0px);
  }
}

@keyframes expand {
  0% {
    transform: translateX(1400px);
  }
  100% {
    transform: translateX(0px);
  }
}

a:link {
  color: red;
  background-color: transparent;
  text-decoration: none;
}
a:visited {
  color: purple;
  background-color: transparent;
  text-decoration: none;
}
a:hover {
  color: blue;
  background-color: transparent;
  text-decoration: underline;
}
a:active {
  color: yellow;
  background-color: transparent;
  text-decoration: underline;
}


@media only screen and (max-width: 700px) { 
    .container_img {
  width: 100%;
  animation: slideIn 1.5s ease-in-out forwards;
  float: left;
}
}
</style>