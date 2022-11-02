<template>
  <div id="app">
    <div class="wrapper">
      <div class="row" v-if="error">
        <div class="column">
          {{ error }}
        </div>
      </div>
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
          <button :disabled="!verified" @click="submitReg">Submit</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import { VueRecaptcha } from "vue-recaptcha";
export default {
  name: "App",
  components: { VueRecaptcha },
  data() {
    return {
      name: "",
      email: "",
      siteKey: "6LfmB9IiAAAAAB9OLZZj83qPRgSdcTbHDwtkeJ82",
      verified: false,
      error: null,
    };
  },
  methods: {
    verifyMethod() {
      this.verified = true;
      alert("verified");
    },
    submitReg() {
      this.error = null;
      axios
        .post("http://54.174.5.102:3001/api/user", {
          name: this.name,
          email: this.email,
        })
        .then((res) => {
          console.log(res.data);
          if (res.data.error) {
            this.error = res.data.message;
          } else {
            this.error = "Successful Registration.";
          }
        });
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

.wrapper {
  width: 80%;
  padding-left: 40px;
  padding-right: 40px;
  padding-top: 20px;
  padding-bottom: 20px;
}

</style>
