<template>
  <div id="app">
    <header>
      <span>Vue.js PWA</span>
    </header>
    <main>
      <img src="./assets/logo.png" alt="Vue.js PWA">
      <!-- <hello></hello> -->
      <div>
        <label>Session</label>
        <input type="text" v-model="session" disabled />
        <button @click="newSession">New Session</button>
      </div>
      <br />
      <form @submit="postInput">
        <label>Type Here</label>
        <input type="text" v-model="reqInput" required/>
        <input type="submit" value="send" />
      </form>
      <p v-html="history">
        {{history}}
      </p>
    </main>
  </div>
</template>

<script>
import Hello from "./components/Hello";

export default {
  name: "app",
  data() {
    return {
      reqInput: "",
      history: "",
      session: "Click To Change >>"
    };
  },
  components: {
    Hello
  },
  methods: {
    newSession: function() {
      var text = "";
      var possible =
        "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789";

      for (var i = 0; i < 5; i++)
        text += possible.charAt(Math.floor(Math.random() * possible.length));

      this.session = text;
      this.history = "";
    },
    postInput: function(e) {
      e.preventDefault();
      this.history += `You say: ${this.reqInput} <br />`;
      var input = this.reqInput;
      this.reqInput = "";
      this.ajaxRequest = true;
      this.$http
        .post("/postRequest", {
          reqInput: input,
          session: this.session
        })
        .then(
          response => {
            // get body data
            this.history += `Response: ${response.body.text} <br />`;

            var audio = new Audio(
              "data:audio/mp3;base64," + response.body.sound
            );
            audio.play();

            console.log(response.body.text);
            // this.someData = response.body;
          },
          response => {
            // error callback
          }
        );
    }
  }
};
</script>

<style>
body {
  margin: 0;
}

#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}

main {
  text-align: center;
  margin-top: 40px;
}

header {
  margin: 0;
  height: 56px;
  padding: 0 16px 0 24px;
  background-color: #35495e;
  color: #ffffff;
}

header span {
  display: block;
  position: relative;
  font-size: 20px;
  line-height: 1;
  letter-spacing: 0.02em;
  font-weight: 400;
  box-sizing: border-box;
  padding-top: 16px;
}
</style>
