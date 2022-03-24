<template>
  <div v-if="post">
   <p>post</p> 
    <div class="blog">
      <img class="blog-image neu-border" :src="post.img" :alt="post.title" />
      <div class="blog-details">
        <h2>{{ post.title }}</h2>
        <p>{{ post.description }}</p>
           <p>{{ post.text }}</p>
        <p>{{ post.category }}</p>
      </div>
    </div>
  </div>
                   <!-- <div v-if="post" >
     <img :src="post.img" class="card_img card1" alt="${post.title}">
     </div>
  <div class="viewport">
   <div class="title">
    <h1> Blogs   </h1> 
   </div>
 <div class="cards" >
   <div class="card">
   
    

     <h3>{{ post.title }}</h3>
      <h5 class="card-category">{{ post.category }}</h5>
     <div class="line">
     </div>
     <p> {{ post.description }} </p>
     <p>Author: {{ post.author }} </p>

      </div>
                 
   </div>

</div> -->
 

     <Loader/>

</template>
<script>
export default {
  props: ["id"],
  data() {
    return {
      post: null,
    };
  },
  mounted() {
    fetch("https://amaarah-blog-backend.herokuapp.com/posts/" + this.id, {
      method: "GET",
      headers: {
        "Content-type": "application/json; charset=UTF-8",
        Authorization: `Bearer ${localStorage.getItem("jwt")}`,
      },
    })
      .then((response) => response.json())
      .then(async (json) => {
        this.post = json;
        await fetch(
          "https://amaarah-blog-backend.herokuapp.com/users" + json.author,
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
            this.post.author_name = json.name;
          });
      });
  },
};
</script>
<style scoped>




 /* #post {
  gap: 20px;
}



@import url('https://fonts.googleapis.com/css?family=Lato');


*{
  margin: 0px;
}

.viewport{
  position:relative;
  background-size: 200% 200%;
  height: auto;
  width:100%;
  -webkit-animation:   AnimationName 10s ease infinite;
-moz-animation: AnimationName 10s ease infinite;
animation: AnimationName 10s ease infinite;
  
}


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
  background-color: #20e6b3;  
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
    height: 200px !important;
  object-fit: cover;
  max-width: 310px 
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
}  */
</style>
