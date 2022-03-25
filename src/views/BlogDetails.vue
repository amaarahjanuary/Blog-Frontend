<template>

<br>
<br>
<br>
<br>
 
  <div v-if="post">
          <h1 class="site-title">{{ post.title }}</h1>
      <p class="site-description"> {{ post.description }} </p>   
  <br>

<img :src="post.img" class="card_img card1" alt="${post.title}">
  <div id="page">
 
  <div class="site-content">
    <div class="content-area">
      <main class="site-main" role="main">
        <article class="post">
          <div class="entry-meta">
            <span class="posted-on"> <p>Author: {{ post.author }} </p></span>
          </div>
          <div class="entry-content">
                <p> {{ post.text }} </p>
          </div>
          <footer class="entry-footer">
            <p>Category: {{ post.category }} </p>
          </footer>
        </article>
        <div class="comments-area">
          <h2 class="comment-title">Comments</h2>
          
          <div class="comment-respond">
            <h2>Leave a Comment</h2>
            <br>
      
            <textarea id="message"></textarea>
            <button>Submit Comment</button>
          </div>
        </div>
      </main>

    </div>
  </div>

</div>

  

 

     <Loader/>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
  </div>
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
            this.post.author = json.name;
          });
      });
  },
};
</script>
<style scoped>




 
/* 
.blog-image{
    height: 400px !important;
  object-fit: cover;
  max-width: 600px 
} */



@import url(https://fonts.googleapis.com/css?family=Old+Standard+TT:400,400italic,700);





a {
  padding-bottom: 2px;
  color: #433F3F;
  text-decoration: none;
  border-bottom: 1px solid #433F3F;
  transition: all .15s ease-in-out;
}
a:hover {
  color: #A34040;
  border-bottom-color: #A34040;
}

#page {
  margin: 120px auto 60px;
  padding: 0 30px;
  max-width: 900px;
}

.site-header {
  text-align: center;
}

.site-header:after {
  display: block;
  content: '';
  margin: 60px auto 90px;
  max-width: 400px;
  border-bottom: 1px solid #D6CCC7;
}

h1.site-title {
  margin: 0 0 10px 0;
  font-size: 50px;
  font-weight: 400;
  text-transform: uppercase;
  letter-spacing: 2px;
  line-height: 1.1;
  padding: 20px;
}
h1.site-title a {
  border: none;
}

p.site-description {
  margin: 0;
  font-size: 16px;
  color: #64625C;
  text-transform: uppercase;
  letter-spacing: 3px;
}

.site-main {
  margin: auto;
  max-width: 640px;
}

.site-main .entry-title,
.site-main .entry-meta {
  text-align: center;
}

h1.entry-title {
  margin: 60px 0 5px 0;
  font-size: 36px;
  font-weight: 400;
  text-transform: uppercase;
  letter-spacing: 1px;
}

.entry-meta .posted-on {
  margin: 0;
  color: #64625C;
  font-size: 18px;
  font-style: italic;
}

.entry-content {
  margin-top: 60px;
  font-size: 22px;
}

.entry-content > p:first-of-type:first-line {
  text-transform: uppercase;
}

.entry-footer {
  margin: 90px 0;
  padding: 30px 0;
  font-size: 18px;
  font-style: italic;
  border-top: 1px solid #D6CCC7;
  border-bottom: 1px solid #D6CCC7;
}
.entry-footer p {
  margin: 0;
}

.comment-area {
  margin-top: 90px;
}

h2.comment-title {
  font-size: 36px;
  font-weight: 400;
  text-transform: uppercase;
  letter-spacing: 2px;
  text-align: center;
}
h2.comment-title:after {
  display: block;
  content: '';
  margin: 30px auto 60px;
  max-width: 300px;
  border-bottom: 1px solid #D6CCC7;  
}

ul.comment-list {
  margin: 0;
  padding: 0;
}

ul.comment-list li {
  margin-bottom: 60px;
  list-style-type: none;
}

ul.comment-list li a {
  display: inline-block;
  padding-bottom: 0px;
  margin-bottom: 5px;
}

.comment-author {
  font-size: 22px;
  font-weight: bold;
}
.comment-author a {
  border-bottom: none;
}

.comment-meta {
  font-size: 16px;
}

.comment-content {
  font-size: 18px;
}

.reply {
  font-size: 18px;
  margin-top: 30px;
}

.comment-respond {
  margin-top: 90px;
}

.comment-reply-title,
.comment-respond input[type="text"] {
  display: block;
  margin-bottom: 5px;
}

.comment-reply-title {
  color: #64625C;
}

.comment-respond input[type="text"] {
  width: 100%;
  margin-bottom: 20px;
  padding: 10px;
  background: #F6F4ED;
  border: 1px solid #D6CCC7;
}

.comment-respond textarea {
  width: 100%;
  padding: 10px;
  height: 200px;
  background: #F6F4ED;
  border: 1px solid #D6CCC7;
}

.comment-respond button {
  margin-top: 20px;
  padding: 15px 30px;
  background: transparent;
  border: 1px solid #D6CCC7;
  font-family: "Old Standard TT", Times New Roman, serif;
  font-size: 16px;
  line-height: 1.5;
  color: #433F3F;
  cursor: pointer;
  transition: background .15s ease-in-out;
}
.comment-respond button:hover {
  background: #D6CCC7;
}

.nav-links {
  margin-top: 150px;
  font-size: 24px;
  font-weight: bold;
  text-transform: uppercase;
  letter-spacing: 1px;
  overflow: auto;
  zoom: 1;
}

.nav-links a {
  padding-bottom: 10px;
  color: #433F3F;
  text-decoration: none;
  border-bottom: none;
}
.nav-links a:hover {
  color: #A34040;
}

.previous-post,
.next-post {
  display: block;
  width: 50%;
}
.previous-post {
  float: left;
  text-align: left;
}
.next-post {
  float: right;
  text-align: right;
}

.site-footer {
  margin-top: 120px;
  text-align: center;
  font-size: 14px;
  line-height: 2;
  text-transform: uppercase;
  letter-spacing: 1px;
}

@media screen and (max-width: 680px) {
  #page {
    margin: 60px auto 30px;
  }
  
  .previous-post,
  .next-post {
    width: 100%;
    float: none;
    text-align: center;
  }
}

.card_img{
    height: 400px !important;
  object-fit: cover;
  max-width: 710px 
}

</style>
