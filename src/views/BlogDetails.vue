<template>
  <div v-if="posts">
    <h2>Blogs</h2>
    <div class="blogs-container" v-if="posts">
      <router-link
        v-for="post of posts"
        :key="post._id"
        :to="{ name: 'BlogDetails', params: { id: post._id } }"
      >
        <img :src="post.img" :alt="post.title" />
        {{ post.author }}
      </router-link>
    </div>
  </div>
  <div v-else>Loading blogs...</div>
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
              "https://amaarah-blog-backend.herokuapp.com/users" + post.author,
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
                post.author = json.name;
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
.blogs-container {
  display: flex;
  flex-wrap: wrap;
  width: 100%;
  margin-inline: auto;
  padding: 30px;
  gap: 2%;
  justify-content: stretch;
  align-items: stretch;
  flex-direction: column;
}

img {
  max-width: 50vw;
}
</style>
