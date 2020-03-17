<template>
  <div id="app">
    <img class="logo" alt="Vue logo" src="./assets/bitcoin-logo.png" />
    <BitcoinWatcher />
    <p class="footer">
      Created by Daniel Kováč &copy; 2020 (Corona pandemic),
      <br />check out the
      <a
        href="https://beatsbysmith.com"
        target="_blank"
        rel="noopener"
      >BeatsBySmith.com</a>.
    </p>
  </div>
</template>

<script>
import BitcoinWatcher from "./components/BitcoinWatcher.vue";

export default {
  name: "App",
  components: {
    BitcoinWatcher
  }
};
</script>

<style>
body {
  background-color: #0b0b0b;
}
.footer{
  color: #7847FF;
}
.footer a{
  color: #7847FF;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.logo {
  width: auto;
  height: 250px;
}
h1 {
  margin: 13px 0;
  font-size: 38px;
}
h3 {
  margin: 3px 0;
  color: #d9ca27;
}
h1,
h2,
h3 {
  font-family: "Abel";
  color: #d9ca27;
}
a,
p {
  font-family: "Abel";
  color: #8c8100;
  margin: 0
}

a:hover {
  font-family: "Abel";
  color: #d9ca27;
}
</style>
