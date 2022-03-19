<template>
 <div class="row align-items-center">
    <div class="col-50">
      <img src="https://i.postimg.cc/zGm9pHqT/tay-Lewis-Collage.png" alt="image">
    </div>
    <div class="col-50">
      <article>
        <h1>About Us</h1>
        <br>
        <p>tayLewis was started in 2022 as a platform to create and show blogs about Taylor Swift and Lewis Hamilton. It's a place where fans of the two can share why they are fans of them and make interesting blogs about them. </p>
        <br>
        <br>
        <p>It's a great environment to find other people who share the same interests as you, as well as introducing you to the fandom. We hope you enjoy the experience on this site and we're looking forward to seeing your contributions to the site. </p>
        <router-link :to="{ name: 'Blogs' }"><div class="btn mt-1 mb-2">See blogs</div></router-link>
      </article>
    </div>
  </div>
</template>

<script>
export default {

}
</script>

<style scoped>
@import url("https://fonts.googleapis.com/css?family=Raleway&display=swap");

* {
  box-sizing: border-box;
}

body {
  font-family: Raleway, sans-serif;
  margin: 0;
  line-height: 1.5;
  font-size: 1rem;
  color: #222;
}

.btn {
  min-width: 200px;
  text-align: center;
  display: inline-block;
  text-decoration: none;
  font-size: 1.4rem;
  border: 2px solid #222;
  padding: 0.3rem 1.2rem;
  text-transform: capitalize;
  color: inherit;
  transition: 0.4s;
}

.btn:hover{
  background-color: #222;
  color: #fff;
}

.col-50,
.col-90 {
  width: 100%;
}

.align-items-center {
  align-items: center;
}

.mt-1{
  margin-top: 1rem;
}

.mb-2{
  margin-bottom: 2rem;
}

@media screen and (min-width: 768px) {
  .row {
    display: flex;
    flex-wrap: wrap;
  }

  .col-50 {
    flex-basis: 50%;
    width: 50%;
  }
}

/*remove block and see change at bottom*/
img {
  display: block;
  width: 100%;
  height: 100vh;
  object-fit: cover;
}

article {
  padding: 0 1.5rem;
  margin-top: 5px;
}

h1 {
  font-size: 3rem;
  letter-spacing: 0.2rem;
  margin-top: -5rem;
  color: #20e6b3;
}

p{
  line-height: 1.6;
}
</style>
