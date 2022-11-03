<template>
  <div id="app" class="row">
    <div class="col-lg-10 col-xl-10 col-md-12 wrapper-holder">
      <div class="row m-0 custom-heading text-center">
        <p class="heading-2">To be invited to the event please let us know by completing your details below.</p>
      </div>
      <div class="row m-0 error-heading" v-if="error">
        <div class="text-center">
          <div v-if="success" class="alert alert-success" role="alert">
            {{ error }}
          </div>
          <div v-else class="alert alert-light" role="alert">
            {{ error }}
          </div>
        </div>
      </div>
      <div class="row m-0" v-if="!success">
        <div class="col-xl-3 col-lg-3 col-sm-6 text-left p-2">
          <div class="input-holder my-2 h-100 button-holder">
            <input
              type="text"
              v-model="name"
              placeholder="Full Name"
              class="form-control border-0"
              tabindex="1"
            />
          </div>
        </div>
        <div class="col-xl-3 col-lg-3 col-sm-6 text-left p-2">
          <div class="input-holder my-2 h-100 button-holder">
            <input
              type="email"
              v-model="email"
              placeholder="Email"
              class="form-control border-0"
              tabindex="2"
            />
          </div>
        </div>
        <div class="col-xl-3 col-lg-3 col-sm-6">
          <div class="button-holder">
            <vue-recaptcha
              :sitekey="siteKey"
              @verify="verifyMethod"
              theme="clean"
              class="recaptcha my-2"
              tabindex="3"
            >
            </vue-recaptcha>
          </div>
        </div>
        <div class="col-xl-2 col-lg-3 col-sm-6">
          <div class="h-100 button-holder">
            <button
              class="btn btn-large btn-light custom-button btn-lg"
              :disabled="!verified"
              @click="submitReg"
              tabindex="4"
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
      success: false,
    };
  },
  methods: {
    verifyMethod() {
      this.verified = true;
    },
    submitReg() {
      this.error = null;
      axios
        .post("https://api.saudi-registration.com/api/user", {
          name: this.name,
          email: this.email,
        })
        .then((res) => {
          if (res.data.error) {
            this.error = "Email already registered.";
          } else {
            this.error = "Successful Registration.";
            this.success = true;
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
  margin-top: 10px;
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
  color: #f3bc86;
  opacity: 1; /* Firefox */
}

input[type="text"]:-ms-input-placeholder,
input[type="email"]:-ms-input-placeholder {
  /* Internet Explorer 10-11 */
  color: #f3bc86;
}

input[type="text"]::-ms-input-placeholder,
input[type="email"]::-ms-input-placeholder {
  /* Microsoft Edge */
  color: #f3bc86;
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
  margin: auto;
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
