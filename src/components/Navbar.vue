<template>
<div class="nav" :class="{ active: isActive }">
  <input type="checkbox" id="nav-check">
  <div class="nav-header">
    <div class="nav-title">
      tayLewis
    </div>
  </div>
  <div class="nav-btn">
    <label for="nav-check">
      <span></span>
      <span></span>
      <span></span>
    </label>
  </div>
  
  <div class="nav-links" >
    <router-link @click="toggleNav" to="/">Home</router-link>
    <router-link @click="toggleNav" :to="{ name: 'About' }">About</router-link>
    <router-link @click="toggleNav" :to="{ name: 'Login' }">Login</router-link>
    <router-link @click="toggleNav" :to="{ name: 'Register' }">Register</router-link>
    <router-link @click="toggleNav" :to="{ name: 'Blogs' }">Blogs</router-link>
    <router-link @click="toggleNav" :to="{ name: 'Profile' }">Profile</router-link>
    <router-link @click="toggleNav" :to="{ name: 'Contact' }">Contact</router-link>
    <router-link @click="logout" class="logout" :to="{ name: 'Home' }">Log out</router-link>
  </div>
</div>
</template>
<script>
export default {
  data() {
    return {
      isActive: false,
    };
  },
  methods: {
    toggleNav() {
      this.isActive = !this.isActive;
    },
    logout() {
      localStorage.clear();
      this.toggleNav;
    },
  },
};

</script>
<style scoped>

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
* {
  box-sizing: border-box;
}

body {
  margin: 0px;
  font-family: 'segoe ui';
}

.nav {
  height: 50px;
  width: 100%;
  background-image: linear-gradient(90deg, #20e6b3, #8e11f3, #4c20d4);
  position: fixed;
    z-index: 100;
      top: 0;
  left: 0;
}


.nav-title {
  text-align: center;
}

.nav > .nav-header {
  display: inline;
}

.nav > .nav-header > .nav-title {
  display: inline-block;
  font-size: 22px;
  color: #fff;
  padding: 10px 10px 10px 10px;
}

.nav > .nav-btn {
  display: none;
}

.nav > .nav-links {
  display: inline;
  float: right;
  font-size: 18px;
}

.nav > .nav-links > a {
  display: inline-block;
  padding: 13px 10px 13px 10px;
  text-decoration: none;
  color: #efefef;
}

.nav > .nav-links > a:hover {
  background-color: rgba(0, 0, 0, 0.3);
}

.nav > #nav-check {
  display: none;
}
 #nav a {
	 font-weight: bold;
	 color: #2c3e50;
	 padding: 20px;
	 text-decoration: none;
}
 .nav a.router-link-exact-active:not(.logout) {
	 color: rgb(0, 195, 255);
}

@media (max-width:600px) {
  .nav > .nav-btn {
    display: inline-block;
    position: absolute;
    right: 0px;
    top: 0px;
  }
  .nav > .nav-btn > label {
    display: inline-block;
    width: 50px;
    height: 50px;
    padding: 13px;
  }
  .nav > .nav-btn > label:hover,.nav  #nav-check:checked ~ .nav-btn > label {
    background-color: rgba(0, 0, 0, 0.3);
  }
  .nav > .nav-btn > label > span {
    display: block;
    width: 25px;
    height: 10px;
    border-top: 2px solid #eee;
  }
  .nav > .nav-links {
    position: absolute;
    display: block;
    width: 100%;
  background-image: linear-gradient(90deg, #20e6b3, #8e11f3, #4c20d4);
    height: 0px;
    transition: all 0.3s ease-in;
    overflow-y: hidden;
    top: 50px;
    left: 0px;
  }
  .nav > .nav-links > a {
    display: block;
    width: 100%;
  }
  .nav > #nav-check:not(:checked) ~ .nav-links {
    height: 0px;
  }
  .nav > #nav-check:checked ~ .nav-links {
    height: calc(100vh - 50px);
    overflow-y: auto;
  }
}

 #nav-links a {
	 font-weight: bold;
	 color: #2c3e50;
	 padding: 20px;
	 text-decoration: none;
}
  .nav.active {
    left: 0;
  }
  /* background-image: linear-gradient(260deg, #e20e0e 0%, #5c0a6b 100%); */
</style>
