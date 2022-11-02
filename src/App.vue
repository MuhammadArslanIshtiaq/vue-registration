<template>
  <div id="app">
    <div class="row">
      <div class="column">
        <input
          type="email"
          placeholder="Email:"
          v-model="email"
          class="input"
        />
      </div>
    </div>
    <div class="row">
      <div class="column">
        <input type="text" placeholder="Name:" v-model="name" class="input" />
      </div>
    </div>
    <div class="row">
      <div class="column">
        <vue-recaptcha
          style="width: none; height: none"
          :sitekey="siteKey"
          @verify="verifyMethod"
          class="recaptcha"
        >
        </vue-recaptcha>
      </div>
    </div>
    <div class="row">
      <div class="column">
        <button>Submit</button>
      </div>
    </div>
  </div>
</template>

<script>
import { VueRecaptcha } from "vue-recaptcha";
export default {
  name: "App",
  components: { VueRecaptcha },
  data() {
    return {
      name: "",
      email: "",
      siteKey: "6LfmB9IiAAAAAB9OLZZj83qPRgSdcTbHDwtkeJ82",
    };
  },
  methods: {
    verifyMethod() {
      alert("verified");
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  margin-top: 60px;
}

.row {
  display: flex;
  flex-direction: column;
  margin-bottom: 30px;
}

.column {
  flex: 50%;
}

.label {
  margin-right: 30px;
  text-align: left;
}

.input {
  height: 30px;
  width: 300px;
  border-radius: 10px;
  border-width: 1px;
  padding: 5px;
}

.recaptcha div {
  margin: auto;
}

button {
  background: #f26e00;
  border-radius: 10px;
  border-color: #f26e00;
  color: white;
  padding: 20px 40px 20px 40px;
}
</style>
