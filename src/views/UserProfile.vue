<template>



<div class="box"  v-for="user of users" :key="user._id" >
  
<h1>{{user.name}}</h1>
<img :src="user.avatar" class="pp" alt="profile-pic">
        <h3>EMAIL:</h3>
<p>{{user.email}}</p>
<h3>CONTACT:</h3>
<p>{{user.contact}}</p>
<h3>PASSWORD:</h3>
<p>{{user.password}}</p>

  <div class="comment-respond">
<button class="btn btn-danger butt">DELETE</button>

<button class="btn btn-secondary butt">EDIT</button>
</div>


</div>
<br>
<br>
<br>


</template>
<script>

export default {

    data() {
    return {
      users: null,
      name:"",
      contact:"",
      email:"",
      avatar: "",
      password: "",

    };
  },
mounted() {
    if (localStorage.getItem("jwt")) {
      fetch("https://amaarah-blog-backend.herokuapp.com/users/"  , {
        method: "GET",
        headers: {
          "Content-type": "application/json; charset=UTF-8",
          Authorization: `Bearer ${localStorage.getItem("jwt")}`,
        },
      })
        .then((response) => response.json())
        .then((json) => {
          this.users = json;
          this.users.forEach(async (user) => {
            await fetch(
              "https://amaarah-blog-backend.herokuapp.com/users/" + user._id,
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
               user._id = json.name;
              });
          });
        })
        .catch((err) => {
          alert("Not logged in");
          this.$router.push({ name: "Login" })
        });
    } else {
      alert("Login failed");
      this.$router.push({ name: "Login" });
    }
    
  },
  
}
</script>

<style scoped>
.box{
  margin: 10px;
  border: 2px solid white;
}
.div2{
  text-align: center;
  margin-left: 43%;
}
.butt{
  margin: 10px;
}

.profile{
   padding-top: 7%;
    padding-bottom: 7%;
    height: 100vh;
   overflow-y: scroll;
}

h1{
  color:#8e11f3;
}

h5,h3{
  color:#20e6b3;
}
p{
  color: white;
}
.nav-link{
  color:white !important;
}
.nav-link:hover{
  color:red !important;
}
.nav-link:focus{
  color:red !important;
}
ul{
  list-style: none;
}
.droppie{
  border: none;
  background: none;
  padding-left: 50px;
}
.droppie:hover{
color: red;
  background: none;
  padding-left: 50px;
}

.pp{
    border-radius: 50%;
    border: solid 2px red;
    object-fit: cover;
    height: 200px;
    width:200px;

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
  background: #8e11f3;
  color: white;
}

.navg{
  position: fixed;
  display: inline-flex;
  right: 5px;
}
@media only screen and (max-width: 500px) {
 .navg{
  position: relative;
  display: initial;
}
.profile{
    padding-top: 15%;
    padding-bottom:15%;
}
.div2{
  text-align: center;
  margin-left: 23%;
}
}
</style>