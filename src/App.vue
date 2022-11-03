<template>
  <div id="app" class="row">
    <div class="col-lg-10 col-xl-10 col-md-12 wrapper-holder">
      <div class="row m-0 custom-heading text-center">
        <p class="heading-2">Sign up here to get access to the stream</p>
      </div>
      <div class="row m-0">
        <div class="col-12 error-heading" v-if="error">
          {{ error }}
        </div>
        <div class="col-xl-3 col-lg-3 col-sm-6 text-left">
          <div class="input-holder p-1 my-2">
            <label for="name" class="">Name</label>
            <input
              type="text"
              placeholder="Full Name:"
              v-model="name"
              class="form-control border-0"
            />
          </div>
        </div>
        <div class="col-xl-3 col-lg-3 col-sm-6 text-left">
          <div class="input-holder p-1 my-2">
            <label for="email">Email</label>
            <input
              type="email"
              placeholder="email@example.com"
              v-model="email"
              class="form-control border-0"
            />
          </div>
        </div>
        <div class="col-xl-3 col-lg-3 col-sm-6">
          <vue-recaptcha
            :sitekey="siteKey"
            @verify="verifyMethod"
            theme="clean"
            class="recaptcha my-2"
          >
          </vue-recaptcha>
        </div>
        <div class="col-xl-2 col-lg-3 col-sm-6">
          <div class="h-100 button-holder">
            <button
              class="btn btn-large btn-light custom-button btn-lg"
              :disabled="!verified"
              @click="submitReg"
            >
              Submit
            </button>
          </div>
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
    },
    submitReg() {
      this.error = null;
      axios
        .post("http://54.174.5.102:3001/api/user", {
          name: this.name,
          email: this.email,
        })
        .then((res) => {
          if (res.data.error) {
            this.error = "Email already registered.";
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
  font-family: "Open sans";
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  background: #ec720c;
  margin-top: 60px;
}
.recaptcha div {
  width: 100% !important;
}

html,
body {
  background: #ec720c;
  width: 100%;
}

.wrapper-holder {
  margin: auto;
}

input {
  background: transparent;
  color: white;
}
input[type="text"],
input[type="email"],
input[type="text"]:focus,
input[type="email"]:focus {
  background-color: transparent;
  border: 0px;
  outline: none;
  -webkit-box-shadow: none;
  -moz-box-shadow: none;
  box-shadow: none;
  color: white;
  cursor: default;
}

input[type="text"]::placeholder,
input[type="email"]::placeholder {
  /* Chrome, Firefox, Opera, Safari 10.1+ */
  color: white;
  opacity: 1; /* Firefox */
}

input[type="text"]:-ms-input-placeholder,
input[type="email"]:-ms-input-placeholder {
  /* Internet Explorer 10-11 */
  color: white;
}

input[type="text"]::-ms-input-placeholder,
input[type="email"]::-ms-input-placeholder {
  /* Microsoft Edge */
  color: white;
}

label {
  text-align: left;
  color: white;
}

.input-holder {
  border: 2px solid white;
  margin: 0;
}
.custom-button {
  color: #ec720c !important;
}
.button-holder {
  display: flex;
  align-items: center;
  justify-content: center;
}
.error-heading,
.custom-heading {
  text-align: center;
  color: white;
}
.custom-heading {
  font-family: "Noto Sans";
  font-size: 32px;
  font-weight: 500;
  line-height: 40px;
  letter-spacing: 0em;
  text-align: left;
}
@media screen and (min-width: 2560px) {
  .button-holder {
    justify-content: left;
  }
}
</style>
