<template>
<br>
<br>
<br>
<br>
  <div v-if="posts">
       <div class="title">
    <h1> Blogs   </h1> 
   </div>

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
          <option value="Both">Both</option>
          <option value="Lewis Hamilton">Lewis Hamilton</option>
          <option value="Taylor Swift">Taylor Swift</option>
        </select>
      </div>
      <div class="d-flex w-25 ms-3">
        <label for="" class="form-label">Sort name</label>
        <select class="form-select" name="" id="sortName" onchange="sortName()">
          <option value="ascending">Ascending</option>
          <option value="descending">Descending</option>
        </select>
      </div>
      <div>


<!-- Search alphabetically -->





<!-- search filter start -->
  <input type="text" v-model="search" placeholder="search blogs" />



<!-- <input type="text" v-model="search" placeholder="search blogs" /> -->
      



 <details>
    <summary class="button">Create a blog</summary>
			
    <div>
 <form >
  <label for="title">Title:</label>
  <input type="text" id="title" name="title" v-model="title"><br><br>
  <label for="category">Category:</label>
    <select id="category" name="category" v-model="category">
    <option value="Lewis Hamilton">Lewis Hamilton</option>
    <option value="Taylor Swift">Taylor Swift</option>
    <option value="Both">Both</option>
  </select><br><br>
  <label for="text">Text:</label>
  <input type="text" id="text" name="text" v-model="text"><br><br>
  <label for="description">Description:</label>
  <input type="text" id="description" name="description" v-model="description"><br><br>
    <label for="img">Image link:</label>
  <input type="text" id="img" name="img" v-model="img"><br><br>
  <label for="author">Author:</label>
  <input type="text" id="author" name="author" v-model="author">
       <div class="comment-respond">
  <button @click="createBlog">
    Create Blog
  </button>
       </div>
       <br>
</form>
    
    </div>




	</details>



      </div>
    </div>
  

<div class="viewport">

 <div class="cards" >
   <div class="card" v-for="post of filterPosts" :key="post.title">
   
    
                 <div v-if="posts" >
     <img :src="post.img" class="card_img card1" alt="${post.title}">
     </div>
     <h3>{{ post.title }}</h3>
      <h5 class="card-category">{{ post.category }}</h5>
     <div class="line">
     </div>
     <p> {{ post.description }} </p>
     <p>Author: {{ post.author }} </p>
     <div class="comment-respond">
       <p>   
         <router-link :to="{ name: 'BlogDetails', params: { id: post._id }}"><button>Read More...</button></router-link> 
       </p>
     </div>
      </div>
                 
   </div>

</div>
 
        



</template>
<script>
export default {
  data() {
    return {
      posts: [],
      title: null,
      category: null,
      description: null,
      text: null,
      img: null,
      author: null,
      search: ""
    };
  },
  methods: {
    // newBlog() {
    //   console.log(localStorage.getItem("jwt"))
    //   fetch("https://amaarah-blog-backend.herokuapp.com/posts", {
    //     method: "POST",
    //     headers: {
    //       "Content-type": "application/json; charset=UTF-8",
    //       Authorization: `Bearer ${localStorage.getItem("jwt")}`,
    //     },
    //     body: JSON.stringify({
    //       title: this.title,
    //       category: this.category,
    //       text: this.text,
    //       description: this.description,
    //       img: this.img,
    //       author: this.author
    //     }),
    //   })
    //   .then((response) => response.json())
    //     .then((json) => {
    //       console.log(json)
    //     })
    //     .catch((err) => {
    //       alert(err);
    //     });
    // },
    createBlog() {
      console.log(localStorage.getItem("jwt"))
      if (!localStorage.getItem("jwt")) {
        alert("User not logged in");
        return this.$router.push({ name: "Login" });
      }
      fetch("https://amaarah-blog-backend.herokuapp.com/posts", {
        method: "POST",
        body: JSON.stringify({
          title: this.title,
          description: this.description,
          category: this.category,
          text: this.text,
          img: this.img,
        }),
        // headers: {
        //   "Content-type": "application/json; charset=UTF-8",
        //   Authorization: `Bearer ${localStorage.getItem("jwt")}`,
        // },
      })
        .then((response) => response.json())
        .then((json) => {
          alert("Blog Created");
          this.$router.push({ name: "Blogs" });
        })
        .catch((err) => {
          alert(err);
        });
    },
  },
  mounted() {
    console.log(localStorage.getItem("jwt"))
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
  computed: {
    filterPosts: function(){
      return this.posts.filter((post) => {
        return post.title.match(this.search);
      })
    }
  }
};
</script>
<style>




#posts {
  gap: 20px;
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
  padding-bottom:50px;
  padding-top:50px;
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

.card_img{
    height: 200px;
  object-fit: cover;
  max-width: 100% 
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

  .card_img{
    height: 200px !important;
  object-fit: cover;
  max-width: 310px 
}
}



/* img {
    height: 200px !important;
  object-fit: cover;
  max-width: 200px 
} */


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

/* pop up modal start */


.button {
  margin-top: 20px;
  padding: 15px 30px;
  background: #20e6b3;
  border: 1px solid #D6CCC7;
  font-family: "Old Standard TT", Times New Roman, serif;
  font-size: 16px;
  line-height: 1.5;
  color: #433F3F;
  cursor: pointer;
  transition: background .15s ease-in-out;
}
.button:hover {
  background: #8e11f3;
  color: white;
}

details > div {
  width: 20em;
  border: 2px solid black;
  padding: 1em 2em;
  position: fixed;
  width: 360px;
  height: 340px;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  margin: auto;
  background: white;
  z-index: 3;
  box-shadow: 10px 10px 10px DIMGRAY;
}

details[open] summary::after { 
  content: "×"; 
  font-size: 28pt;  
  position: fixed; 
  right: calc(50vw - 360px / 2 - 2em); 
  top:  calc(50vh - 240px / 2 - 2em);
  padding: 5pt 10pt;
  z-index: 9;
}

details[open] summary::before {
  content: '';
  display: block;
  width: 10px;
  height: 10px;
  background: black;
  position: fixed;
  top: 0;
  left: 0;
  opacity: 0.5;
  z-index: 1;
}





.neu-border {
  border-radius: 30px;

}
.neu-border-inset {
  border-radius: 30px;

}

h4 {
    margin-top: -10px;
}

.form {
  display: flex;
  flex-direction: column;
  justify-content: center;
  padding: 30px;
  gap: 20px;
  width: 100%;
  margin-inline: auto;
  max-width: 600px;
  margin-top: 100px;
  background-color: #8500e4;
  color: white;
  margin-bottom: 20px;
  max-height: 800px;
}

.form-heading {
  text-align: center;
  text-transform: uppercase;
  font-size: 40px;
  padding-bottom: 10px;
}

.form-input,
.form-btn {
  border: none;
  outline: none;
  padding: 20px;
}

.form-btn {
  cursor: pointer;
  transition: all 0.1s linear;
}

.form-btn:hover {
  transform: scale(1.05);
}

.form-social-login {
  display: flex;
  justify-content: space-between;
}

.form-social-btn {
  width: 45%;
  color: white;
}

/* pop up modal ends */

.comment-respond button {
  margin-top: 20px;
  padding: 15px 30px;
  background: white;
  border: 1px solid #D6CCC7;
  font-family: "Old Standard TT", Times New Roman, serif;
  font-size: 16px;
  line-height: 1.5;
  color: #433F3F;
  cursor: pointer;
  transition: background .15s ease-in-out;
}
.comment-respond button:hover {
  background: #8e11f3;
  color: white;
}
</style>
