<template>
  <form @submit.prevent="handleSubmit">
      <h2 class="form-heading">Contact Us</h2>
          <h4>Get in contact with us</h4>
      <input type="name" required v-model="name" placeholder="Full Name">


      <input type="email" required v-model="email" placeholder="Email">

      <label>Write us a message below</label>
      <br>
      <textarea name="message" id="message" rows="5" v-model="message" class="message"></textarea>

      



<div class="submit">
    <button type="submit">Send Message</button>
</div>

  </form>

  <!-- <p>Name: {{ name }}</p>
  <p>Email: {{ email }}</p>
  <p>Message: {{ message }}</p> -->

</template>

<script>
    export default {
        data() {
            return {
                name: '',
                email: '',
                message: ''
            }
        },
        methods: {
            handleSubmit() {
                console.log(this.name, this.email, this,message);
                fetch("https://amaarah-blog-backend.herokuapp.com/", {
                    method: "POST", 
                    body: JSON.stringify({
                        name: this.name, 
                        email: this.email, 
                        message: this.message
                    }), 
                    headers: {
                        "Content-Type": "application/json; charset=UTF-8"
                    },
                })
                .then((response) => response.json())
                .then((json) => alert(json.msg))
                .catch((e) => alert(e.msg))
                }
            }
        }

</script>

<style scoped>
form {
  display: flex;
  flex-direction: column;
  justify-content: center;
  padding: 30px;
  gap: 20px;
  width: 100%;
  margin-inline: auto;
  max-width: 600px;
  margin-top: 200px;
  background-color: #8500e5;
  color: white;
  border-radius: 30px;
  padding-bottom: 10px;
    margin-top: 200px;
}

.form-heading {
  text-align: center;
  text-transform: uppercase;
  font-size: 40px;
  padding-bottom: 10px;
  color: #20e6b3;
}

label {
    color: white;
    display: inline-block;
    margin: 25px 0 5px 0;
    font-size: 1em;
    letter-spacing: 1px;
    font-weight: bold;
    border-radius: 30px;
    font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;
    margin-bottom: -20px;
}
input, select {
    display: block;
    padding: 10px 6px;
    width: 100%;
    box-sizing: border-box;
    border: none;
    border-bottom: 1px solid #ddd;
    color: #555;
      border-radius: 30px;
}
input[type="checkbox"] {
    display: inline-block;
    width: 16px;
    margin: 0 10px 0 0;
    position: relative;
    top: 2px;
}
.pill {
    display: inline-block;
    margin: 20px 10px 0 0;
    padding: 6px 12px;
    background: #eee;
    border-radius: 20px;
    font-size: 12px;
    letter-spacing: 1px;
    font-weight: bold;
    color: #777;
    cursor: pointer;
}
button {
    background: #0b6dff;
    border: 0;
    padding: 10px 20px;
    margin-top: 20px;
    color: white;
    border-radius: 20px;
}
.submit {
    text-align: center;
}
.error {
    color: #ff0062;
    margin-top: 10px;
    font-size: 0.8em;
    font-weight: bold;
}
textarea {
      resize: none;
      width: 100%;
      height: 100px;
      border-radius: 30px;
}

#message {
     font-size: 0.9em;
}
</style>