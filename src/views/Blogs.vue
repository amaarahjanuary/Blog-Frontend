<template>
  <div v-if="posts">
    <h2>Blogs</h2>

  </div>
  <div v-else>Loading blogs...</div>
    <div class="container d-flex justify-content-end mb-3 mt-5 pt-4">
      <div class="d-flex w-25 ms-3">
        <label for="" class="form-label">Sort by category</label>
        <select
          class="form-select"
          name=""
          id="sortCategory"
          onchange="sortCategory()"
        >
          <option value="All">All</option>
          <option value="Footwear">Footwear</option>
          <option value="Clothing">Clothing</option>
        </select>
      </div>
      <div class="d-flex w-25 ms-3">
        <label for="" class="form-label">Sort name</label>
        <select class="form-select" name="" id="sortName" onchange="sortName()">
          <option value="ascending">Ascending</option>
          <option value="descending">Descending</option>
        </select>
      </div>

    </div>
    
<div class="viewport">
   <div class="title">
    <h1> Blogs   </h1> 
   </div>
 <div class="cards">
  
   <div class="card">
     <div class="card_img card1">
          <div class="plus"><p>+</p></div>
     </div>
     <h3>AMAZING FLUO</h3>
     <div class="line">
     </div>
     <p> Sed ut perspiciatis unde omnis iste natus error sit voluptatem accusantium doloremque laudantium.  </p>
     
    
   </div>
   <div class="card">
     <div class="card_img card2">
       <div class="plus"><p>+</p></div>
     </div>
     <h3>TITLE HERE</h3>
     <div class="line">
     </div>
    <p> Sed ut perspiciatis unde omnis iste natus error sit voluptatem accusantium doloremque laudantium, totam rem aperiam.</p>
   </div>
   <div class="card">
     <div class="card_img card3">
       <div class="plus"><p>+</p></div>
     </div>
     <h3>TITLE HERE</h3>
     <div class="line">
     </div>
     <p>Eaque ipsa quae ab illo inventore veritatis et quasi architecto beatae vitae dicta sunt explicabo.</p>
   </div>
   <div class="card">
     <div class="card_img card4">
       <div class="plus"><p>+</p></div>
     </div>
     <h3>TITLE HERE</h3>
     <div class="line">
     </div>
     <p>voluptatem accusantium doloremque laudantium, totam rem aperiam, eaque ipsa quae ab illo inventore veritatis et quasi architecto beatae vitae dicta sunt explicabo.</p></div>
   <div class="card">
     <div class="card_img card5">
       <div class="plus"><p>+</p></div>
     </div>
     <h3>TITLE HERE</h3>
     <div class="line">
     </div>
    <p> Sed ut perspiciatis unde omnis iste natus error sit voluptatem accusantium doloremque laudantium, totam rem aperiam, eaque ipsa quae ab illo inventore veritatis et quasi.</p>
   </div>
   <div class="card">
     <div class="card_img card6">
       <div class="plus"><p>+</p></div>
     </div>
     <h3>TITLE HERE</h3>
     <div class="line">
     </div>
     <p> Sed ut perspiciatis unde omnis iste natus error sit voluptatem accusantium doloremque laudantium, totam rem aperiam, eaque ipsa quae ab illo inventore veritatis et quasi architecto beatae vitae dicta sunt explicabo.  </p>
   </div>
</div>
</div>
 
          



</template>
<script>
export default {
  data() {
    return {
      posts: null,
    };
  },
  mounted() {
    if (localStorage.getItem("jwt")) {
      fetch("https://amaarah-blog-backend.herokuapp.com/posts", {
        method: "GET",
        headers: {
          "Content-type": "application/json; charset=UTF-8",
          Authorization: `Bearer ${localStorage.getItem("jwt")}`,
        },
      })
        .then((response) => response.json())
        .then((json) => {
          this.posts = json;
          this.posts.forEach(async (post) => {
            await fetch(
              "https://amaarah-blog-backend.herokuapp.com/users" + post.title,
              {
                method: "GET",
                headers: {
                  "Content-type": "application/json; charset=UTF-8",
                  Authorization: `Bearer ${localStorage.getItem("jwt")}`,
                },
              }
            )
              .then((response) => response.json())
              .then((json) => {
                post.title = json.name;
              });
          });
        })
        .catch((err) => {
          alert("User not logged in");
        });
    } else {
      alert("User not logged in");
      this.$router.push({ name: "Login" });
    }
  },
};
</script>
<style>




#posts {
  gap: 20px;
}

img {
    height: 200px !important;
  object-fit: cover;
  max-width: 200px 
}

@import url('https://fonts.googleapis.com/css?family=Lato');


*{
  margin: 0px;
}

.viewport{
  position:relative;
  /* background: linear-gradient(90deg, #20e6b3, #8e11f3, #4c20d4); */
  background-size: 200% 200%;
  height: auto;
  width:100%;
  -webkit-animation:   AnimationName 10s ease infinite;
-moz-animation: AnimationName 10s ease infinite;
animation: AnimationName 10s ease infinite;
  
}

/* @-webkit-keyframes AnimationName {
    0%{background-position:0% 50%}
    50%{background-position:100% 50%}
    100%{background-position:0% 50%}
}
@-moz-keyframes AnimationName {
    0%{background-position:0% 50%}
    50%{background-position:100% 50%}
    100%{background-position:0% 50%}
}
@keyframes AnimationName { 
    0%{background-position:0% 50%}
    50%{background-position:100% 50%}
    100%{background-position:0% 50%}
} */

.card p{
  font-family: lato;
  margin:0px;
  color: black;
  font-weight: 400;
  font-size:15px;
  line-height:90%;
  padding-left: 8%;
  padding-right: 8%;
  padding-top:3%;
  padding-bottom:8%;
  border-radius:20px;
  cursor:pointer;
  transition: ease 1s;
  -webkit-transition: ease 1s;
}

.card h3{
  font-family: lato;
  margin:0px;
  color: black;
  font-weight: 400;
  font-size:20px;
  line-height:90%;
  padding-left: 8%;
  padding-top:8%;
  padding-bottom:3%;
  border-radius:20px;
  cursor:pointer;
  transition: ease 1s;
  -webkit-transition: ease 1s;
}

h1{
  font-family: lato;
  color:#8e11f3;
  font-weight: 400;
  font-size:35px;
  line-height:90%;
  padding-bottom:140px;
  padding-top:150px;
  position:relative;
  text-align:center;
  
}

.title{
  width:78%;
  margin:auto;
  padding-left:0px;
  padding-bottom:0px;
}

.cards{
  width:80%;
  position:relative;
  margin-left:auto;
  margin-right:auto;
  padding-bottom:200px;
  display:flex;
  flex-direction: row;
  flex-wrap: wrap;
  
}

.card{
  width:22%;
  position:relative;
  background-color:white;
  margin:1.13%;
  border-radius:5px;
  transition: 1s;
  -webkit-transition:0.5s;
  cursor:pointer;
    flex: 1 1 auto;
}

.card:hover{
  transform: scale(1.05);
  box-shadow: 10px 10px 15px rgba(0,0,0,0.3);
}

@media screen and (max-width: 1200px){
  .card{
  width:30%;
  margin:1.6%;
  }
}

@media screen and (max-width: 800px){
  .card{
  width:45%;
  margin:2.5%;
  }
}

@media screen and (max-width: 500px){
  .card{
  width:98%;
  margin:2%;
  }
}

.card_img{
  width:100%;
  height:150px;
  position:reltive;
  border-radius: 5px 5px 0px 0px;
  background-size: cover;
  background-position:center center; 
  background-color: #20e6b3;
  transition:1s;
  -webkit-transition:1s;
}

.card1{
   background-image: url(http://www.festabimbianimazione.it/media/k2/galleries/136/Colori%20Fluo%20festa%20Arezzo%207.JPG);
}
.card2{
   background-image: url(https://encrypted-tbn2.gstatic.com/images?q=tbn:ANd9GcQvdIMVlW3Mn8TmkGmtulq2taIDoUIJvr_lt87EWhgdCY5diNhH0Q);
}
.card3{
   background-image: url(http://www.romatoday.it/~media/horizontal-hi/26065597680895/fluo-party-2-2.jpg);
}
.card4{
   background-image: url(https://encrypted-tbn2.gstatic.com/images?q=tbn:ANd9GcSiLXTcanAKRZhMo-5Ga9pzsXIgjWcSbCdz3xFhMVI1PDZSRgQgUQ);
}
.card5{
   background-image: url(https://www.gadgetsvirali.com/wp-content/uploads/2016/09/preservativo-fluo-thumbnail-1.jpg);
}
.card6{
   background-image: url(http://www.festabimbianimazione.it/media/k2/galleries/136/Colori%20Fluo%20festa%20Arezzo%207.JPG);
}

.line{
  height:2px;
  width:84%;
  margin:auto;
  background-color: #8e11f3;
}

.title input{
  background: transparent;
  border:1px solid white;
  padding-top:10px;
  padding-bottom:10px;
  padding-left:20px;
  display:inline;
  font-family: lato;
  color: white;
  font-size:18px;
  line-height:90%;
  border-radius:30px;
  width:150px;
  float:right;
  margin-top:30px;
}

.title textarea:focus, input:focus{
    outline: none;
}

.plus{
  width:20px;
  height:20px;
  background: transparent;
  border-radius: 50%;
  position: absolute;
  border: 2px solid white;
  top:10px;
  right:10px;
  transition: 1s;
  -webkit-transition: 1s;
}

.plus:hover{
  transform: scale(1.1) rotate(90deg);
}

.plus p{
  padding: 0px !important;
  display:inline;
  margin:0px;
  line-height:50%;
  left:50%;
  top:45.3%;
  transform:translate(-50%,-50%);
  position:absolute;
  color: white;
}

.zoomed{
  width:100%;
}

</style>
