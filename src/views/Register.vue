
<template>
  <form @submit.prevent="register" class="form neu-border">
    <h2 class="form-heading">Register</h2>
    <h4>Create your account now</h4>
    <input
      class="form-input neu-border-inset"
      type="text"
      v-model="name"
      placeholder="Full Name"
    />
    <input
      class="form-input neu-border-inset"
      type="email"
      v-model="email"
      placeholder="Email Address"
    />
    <input
      class="form-input neu-border-inset"
      type="text"
      v-model="contact"
      placeholder="Contact Number"
    />
        <input
      class="form-input neu-border-inset"
      type="text"
      v-model="avatar"
      placeholder="Profile pic"
    />
    <input
      class="form-input neu-border-inset"
      type="password"
      v-model="password"
      placeholder="Password"
    />
     <div class="comment-respond">
    <button type="submit" class="button">Sign up</button>
     </div>

    <p>
      Already have an account?
      <router-link :to="{ name: 'Login' }"><div class="link">Sign in</div></router-link>
    </p>
  </form>
</template>

<script>
export default {
  data() {
    return {
      name: "",
      email: "",
      contact: "",
      avatar:"",
      password: "",
    };
  },
  methods: {
    register() {
      fetch("https://amaarah-blog-backend.herokuapp.com/users", {
        method: "POST",
        body: JSON.stringify({
          name: this.name,
          email: this.email,
          contact: this.contact,
          avatar: this.avatar,
          password: this.password,
        }),
        headers: {
          "Content-type": "application/json; charset=UTF-8",
        },
      })
        .then((response) => response.json())
        .then((json) => {
          this.msg = `${ this.name } registered Successfully`;
          alert("User registered. Redirecting to Login...");
          localStorage.setItem("jwt", json.jwt);
          this.$router.push({ name: "Login" });
        })
        .catch((err) => {
          alert(err);
        });
    },
  },
};
</script>

<style scoped>
/* body {
  background: linear-gradient(0deg, rgba(0, 0, 0, 0.7), rgba(0, 0, 0, 0.7)),
    url("https://images.pexels.com/photos/5709615/pexels-photo-5709615.jpeg?auto=compress&cs=tinysrgb&dpr=2&h=650&w=940");
} */
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
}

.form-heading {
  text-align: center;
  text-transform: uppercase;
  font-size: 40px;
  padding-bottom: 10px;
  color: #20e6b3;
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

.link {
  color: #20e6b3;
}

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
    border-radius: 30px;
}
.comment-respond button:hover {
  background: #20e6b3;
  color: white;
}
</style>