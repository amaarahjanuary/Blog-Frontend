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

<a href="https://www.instagram.com/taylewisblog/" class="icon-instagram icon-blue icon-btn" target="_blank"></a>
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


/* icon */

@import url(https://netdna.bootstrapcdn.com/font-awesome/4.0.3/css/font-awesome.min.css);
@import url(//netdna.bootstrapcdn.com/font-awesome/3.2.1/css/font-awesome.min.css);
* {
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
  box-sizing: border-box;
}

html {
  width: 100%;
  height: 100%;
}

body {
  width: 100%;
  height: 100%;
  display: box;
  box-align: center;
  box-pack: center;
  transform: translate3d(0, 0, 0);
}

.clearfix {
  zoom: 1;
}
.clearfix:before, .clearfix:after {
  content: "\0020";
  display: block;
  height: 0;
  overflow: hidden;
}
.clearfix:after {
  clear: both;
}

body {
  background-image: url('data:image/svg+xml;base64,PD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZGluZz0idXRmLTgiPz4gPHN2ZyB2ZXJzaW9uPSIxLjEiIHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8yMDAwL3N2ZyI+PGRlZnM+PGxpbmVhckdyYWRpZW50IGlkPSJncmFkIiBncmFkaWVudFVuaXRzPSJvYmplY3RCb3VuZGluZ0JveCIgeDE9IjAuMCIgeTE9IjAuMCIgeDI9IjEuMCIgeTI9IjEuMCI+PHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iI2IyNmVkZCIgc3RvcC1vcGFjaXR5PSIwLjI1Ii8+PHN0b3Agb2Zmc2V0PSIxMDAlIiBzdG9wLWNvbG9yPSIjM2RjNmQyIiBzdG9wLW9wYWNpdHk9IjAuNSIvPjwvbGluZWFyR3JhZGllbnQ+PC9kZWZzPjxyZWN0IHg9IjAiIHk9IjAiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiIGZpbGw9InVybCgjZ3JhZCkiIC8+PC9zdmc+IA==');
  background-size: 100%;
  background-image: -webkit-gradient(linear, 0% 0%, 100% 100%, color-stop(0%, rgba(178, 110, 221, 0.25)), color-stop(100%, rgba(61, 198, 210, 0.5)));
  background-image: -moz-linear-gradient(left top, rgba(178, 110, 221, 0.25), rgba(61, 198, 210, 0.5));
  background-image: -webkit-linear-gradient(left top, rgba(178, 110, 221, 0.25), rgba(61, 198, 210, 0.5));
  background-image: linear-gradient(to right bottom, rgba(178, 110, 221, 0.25), rgba(61, 198, 210, 0.5));
}

.icon-btn {
  text-align: center;
  font-size: 2em;
  color: rgba(255, 255, 255, 0.75);
  display: inline-block;
  text-decoration: none;
  width: 2em;
  height: 2em;
  padding: 0.5em 0;
  border-radius: 100%;
  position: relative;
  text-shadow: 0 0.025em 0.025em rgba(0, 0, 0, 0.2);
  border: 0.025em solid rgba(0, 0, 0, 0.05);
  background-repeat: repeat-x;
  background-position: 0 0;
  -moz-background-origin: border;
  -o-background-origin: border-box;
  -webkit-background-origin: border;
  background-origin: border-box;
  -moz-transition: background-position 0.1s linear;
  -o-transition: background-position 0.1s linear;
  -webkit-transition: background-position 0.1s linear;
  transition: background-position 0.1s linear;
}
.icon-btn:hover {
  background-position: 0 -2em;
  -moz-transition: background-position 0.1s linear;
  -o-transition: background-position 0.1s linear;
  -webkit-transition: background-position 0.1s linear;
  transition: background-position 0.1s linear;
}

.icon-blue {
  background-color: #3dadd2;
  background-image: url('data:image/svg+xml;base64,PD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZGluZz0idXRmLTgiPz4gPHN2ZyB2ZXJzaW9uPSIxLjEiIHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8yMDAwL3N2ZyI+PGRlZnM+PGxpbmVhckdyYWRpZW50IGlkPSJncmFkIiBncmFkaWVudFVuaXRzPSJvYmplY3RCb3VuZGluZ0JveCIgeDE9IjAuNSIgeTE9IjAuMCIgeDI9IjAuNSIgeTI9IjEuMCI+PHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iIzZlZGRkNyIvPjxzdG9wIG9mZnNldD0iMTAwJSIgc3RvcC1jb2xvcj0iIzNkYWRkMiIvPjwvbGluZWFyR3JhZGllbnQ+PC9kZWZzPjxyZWN0IHg9IjAiIHk9IjAiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiIGZpbGw9InVybCgjZ3JhZCkiIC8+PC9zdmc+IA==');
  background-size: 100%;
  background-image: -webkit-gradient(linear, 50% 0%, 50% 100%, color-stop(0%, #6eddd7), color-stop(100%, #3dadd2));
  background-image: -moz-linear-gradient(top, #6eddd7, #3dadd2);
  background-image: -webkit-linear-gradient(top, #6eddd7, #3dadd2);
  background-image: linear-gradient(to bottom, #6eddd7, #3dadd2);
}

.icon-red {
  background-color: #e1534f;
  background-image: url('data:image/svg+xml;base64,PD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZGluZz0idXRmLTgiPz4gPHN2ZyB2ZXJzaW9uPSIxLjEiIHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8yMDAwL3N2ZyI+PGRlZnM+PGxpbmVhckdyYWRpZW50IGlkPSJncmFkIiBncmFkaWVudFVuaXRzPSJvYmplY3RCb3VuZGluZ0JveCIgeDE9IjAuNSIgeTE9IjAuMCIgeDI9IjAuNSIgeTI9IjEuMCI+PHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iI2UwOTY2ZiIvPjxzdG9wIG9mZnNldD0iMTAwJSIgc3RvcC1jb2xvcj0iI2UxNTM0ZiIvPjwvbGluZWFyR3JhZGllbnQ+PC9kZWZzPjxyZWN0IHg9IjAiIHk9IjAiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiIGZpbGw9InVybCgjZ3JhZCkiIC8+PC9zdmc+IA==');
  background-size: 100%;
  background-image: -webkit-gradient(linear, 50% 0%, 50% 100%, color-stop(0%, #e0966f), color-stop(100%, #e1534f));
  background-image: -moz-linear-gradient(top, #e0966f, #e1534f);
  background-image: -webkit-linear-gradient(top, #e0966f, #e1534f);
  background-image: linear-gradient(to bottom, #e0966f, #e1534f);
}

.icon-purple {
  background-color: #6b4fe1;
  background-image: url('data:image/svg+xml;base64,PD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZGluZz0idXRmLTgiPz4gPHN2ZyB2ZXJzaW9uPSIxLjEiIHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8yMDAwL3N2ZyI+PGRlZnM+PGxpbmVhckdyYWRpZW50IGlkPSJncmFkIiBncmFkaWVudFVuaXRzPSJvYmplY3RCb3VuZGluZ0JveCIgeDE9IjAuNSIgeTE9IjAuMCIgeDI9IjAuNSIgeTI9IjEuMCI+PHN0b3Agb2Zmc2V0PSIwJSIgc3RvcC1jb2xvcj0iI2E5NmZlMCIvPjxzdG9wIG9mZnNldD0iMTAwJSIgc3RvcC1jb2xvcj0iIzZiNGZlMSIvPjwvbGluZWFyR3JhZGllbnQ+PC9kZWZzPjxyZWN0IHg9IjAiIHk9IjAiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiIGZpbGw9InVybCgjZ3JhZCkiIC8+PC9zdmc+IA==');
  background-size: 100%;
  background-image: -webkit-gradient(linear, 50% 0%, 50% 100%, color-stop(0%, #a96fe0), color-stop(100%, #6b4fe1));
  background-image: -moz-linear-gradient(top, #a96fe0, #6b4fe1);
  background-image: -webkit-linear-gradient(top, #a96fe0, #6b4fe1);
  background-image: linear-gradient(to bottom, #a96fe0, #6b4fe1);
}


/* icon end */
</style>