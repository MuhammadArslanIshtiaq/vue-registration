<template>
  <div id="app" class="row">
    <div class="col-lg-10 col-xl-10 col-md-12 wrapper-holder">
      <div class="row m-0 custom-heading text-center">
        <p class="heading-2">
          To be invited to the event please let us know by completing your
          details below.
        </p>
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
@font-face {
  font-family: "Futura PT";
  src: url("./assets/FuturaPT-Bold.eot");
  src: local("Futura PT Bold"), local("FuturaPT-Bold"),
    url("./assets/FuturaPT-Bold.eot?#iefix") format("embedded-opentype"),
    url("./assets/FuturaPT-Bold.woff2") format("woff2"),
    url("./assets/FuturaPT-Bold.woff") format("woff"),
    url("./assets/FuturaPT-Bold.ttf") format("truetype");
  font-weight: bold;
  font-style: normal;
}

@font-face {
  font-family: "Futura PT";
  src: url("./assets/FuturaPT-Heavy.eot");
  src: local("Futura PT Heavy"), local("FuturaPT-Heavy"),
    url("./assets/FuturaPT-Heavy.eot?#iefix") format("embedded-opentype"),
    url("./assets/FuturaPT-Heavy.woff2") format("woff2"),
    url("./assets/FuturaPT-Heavy.woff") format("woff"),
    url("./assets/FuturaPT-Heavy.ttf") format("truetype");
  font-weight: 900;
  font-style: normal;
}

@font-face {
  font-family: "Futura PT Demi";
  src: url("./assets/FuturaPT-DemiObl.eot");
  src: local("Futura PT Demi Oblique"), local("FuturaPT-DemiObl"),
    url("./assets/FuturaPT-DemiObl.eot?#iefix") format("embedded-opentype"),
    url("./assets/FuturaPT-DemiObl.woff2") format("woff2"),
    url("./assets/FuturaPT-DemiObl.woff") format("woff"),
    url("./assets/FuturaPT-DemiObl.ttf") format("truetype");
  font-weight: 600;
  font-style: italic;
}

@font-face {
  font-family: "Futura PT Cond Extra";
  src: url("./assets/FuturaPTCond-ExtraBoldObl.eot");
  src: local("Futura PT Cond Extra Bold Oblique"),
    local("FuturaPTCond-ExtraBoldObl"),
    url("./assets/FuturaPTCond-ExtraBoldObl.eot?#iefix") format("embedded-opentype"),
    url("./assets/FuturaPTCond-ExtraBoldObl.woff2") format("woff2"),
    url("./assets/FuturaPTCond-ExtraBoldObl.woff") format("woff"),
    url("./assets/FuturaPTCond-ExtraBoldObl.ttf") format("truetype");
  font-weight: 800;
  font-style: italic;
}

@font-face {
  font-family: "Futura PT Cond Book";
  src: url("./assets/FuturaPTCond-Book.eot");
  src: local("Futura PT Cond Book"), local("FuturaPTCond-Book"),
    url("./assets/FuturaPTCond-Book.eot?#iefix") format("embedded-opentype"),
    url("./assets/FuturaPTCond-Book.woff2") format("woff2"),
    url("./assets/FuturaPTCond-Book.woff") format("woff"),
    url("./assets/FuturaPTCond-Book.ttf") format("truetype");
  font-weight: normal;
  font-style: normal;
}

@font-face {
  font-family: "Futura PT";
  src: url("./assets/FuturaPT-LightObl.eot");
  src: local("Futura PT Light Oblique"), local("FuturaPT-LightObl"),
    url("./assets/FuturaPT-LightObl.eot?#iefix") format("embedded-opentype"),
    url("./assets/FuturaPT-LightObl.woff2") format("woff2"),
    url("./assets/FuturaPT-LightObl.woff") format("woff"),
    url("./assets/FuturaPT-LightObl.ttf") format("truetype");
  font-weight: 300;
  font-style: italic;
}

@font-face {
  font-family: "Futura PT Book";
  src: url("./assets/FuturaPT-BookObl.eot");
  src: local("Futura PT Book Oblique"), local("FuturaPT-BookObl"),
    url("./assets/FuturaPT-BookObl.eot?#iefix") format("embedded-opentype"),
    url("./assets/FuturaPT-BookObl.woff2") format("woff2"),
    url("./assets/FuturaPT-BookObl.woff") format("woff"),
    url("./assets/FuturaPT-BookObl.ttf") format("truetype");
  font-weight: normal;
  font-style: italic;
}

@font-face {
  font-family: "Futura PT";
  src: url("./assets/FuturaPT-HeavyObl.eot");
  src: local("Futura PT Heavy Oblique"), local("FuturaPT-HeavyObl"),
    url("./assets/FuturaPT-HeavyObl.eot?#iefix") format("embedded-opentype"),
    url("./assets/FuturaPT-HeavyObl.woff2") format("woff2"),
    url("./assets/FuturaPT-HeavyObl.woff") format("woff"),
    url("./assets/FuturaPT-HeavyObl.ttf") format("truetype");
  font-weight: 900;
  font-style: italic;
}

@font-face {
  font-family: "Futura PT Cond";
  src: url("./assets/FuturaPTCond-BoldObl.eot");
  src: local("Futura PT Cond Bold Oblique"), local("FuturaPTCond-BoldObl"),
    url("./assets/FuturaPTCond-BoldObl.eot?#iefix") format("embedded-opentype"),
    url("./assets/FuturaPTCond-BoldObl.woff2") format("woff2"),
    url("./assets/FuturaPTCond-BoldObl.woff") format("woff"),
    url("./assets/FuturaPTCond-BoldObl.ttf") format("truetype");
  font-weight: bold;
  font-style: italic;
}

@font-face {
  font-family: "Futura PT Demi";
  src: url("./assets/FuturaPT-Demi.eot");
  src: local("Futura PT Demi"), local("FuturaPT-Demi"),
    url("./assets/FuturaPT-Demi.eot?#iefix") format("embedded-opentype"),
    url("./assets/FuturaPT-Demi.woff2") format("woff2"),
    url("./assets/FuturaPT-Demi.woff") format("woff"),
    url("./assets/FuturaPT-Demi.ttf") format("truetype");
  font-weight: 600;
  font-style: normal;
}

@font-face {
  font-family: "Futura PT Cond Book";
  src: url("./assets/FuturaPTCond-BookObl.eot");
  src: local("Futura PT Cond Book Oblique"), local("FuturaPTCond-BookObl"),
    url("./assets/FuturaPTCond-BookObl.eot?#iefix") format("embedded-opentype"),
    url("./assets/FuturaPTCond-BookObl.woff2") format("woff2"),
    url("./assets/FuturaPTCond-BookObl.woff") format("woff"),
    url("./assets/FuturaPTCond-BookObl.ttf") format("truetype");
  font-weight: normal;
  font-style: italic;
}

@font-face {
  font-family: "Futura PT Extra";
  src: url("./assets/FuturaPT-ExtraBold.eot");
  src: local("Futura PT Extra Bold"), local("FuturaPT-ExtraBold"),
    url("./assets/FuturaPT-ExtraBold.eot?#iefix") format("embedded-opentype"),
    url("./assets/FuturaPT-ExtraBold.woff2") format("woff2"),
    url("./assets/FuturaPT-ExtraBold.woff") format("woff"),
    url("./assets/FuturaPT-ExtraBold.ttf") format("truetype");
  font-weight: 800;
  font-style: normal;
}

@font-face {
  font-family: "Futura PT Cond";
  src: url("./assets/FuturaPTCond-Medium.eot");
  src: local("Futura PT Cond Medium"), local("FuturaPTCond-Medium"),
    url("./assets/FuturaPTCond-Medium.eot?#iefix") format("embedded-opentype"),
    url("./assets/FuturaPTCond-Medium.woff2") format("woff2"),
    url("./assets/FuturaPTCond-Medium.woff") format("woff"),
    url("./assets/FuturaPTCond-Medium.ttf") format("truetype");
  font-weight: 500;
  font-style: normal;
}

@font-face {
  font-family: "Futura PT";
  src: url("./assets/FuturaPT-Medium.eot");
  src: local("Futura PT Medium"), local("FuturaPT-Medium"),
    url("./assets/FuturaPT-Medium.eot?#iefix") format("embedded-opentype"),
    url("./assets/FuturaPT-Medium.woff2") format("woff2"),
    url("./assets/FuturaPT-Medium.woff") format("woff"),
    url("./assets/FuturaPT-Medium.ttf") format("truetype");
  font-weight: 500;
  font-style: normal;
}

@font-face {
  font-family: "Futura PT Cond Extra";
  src: url("./assets/FuturaPTCond-ExtraBold.eot");
  src: local("Futura PT Cond Extra Bold"), local("FuturaPTCond-ExtraBold"),
    url("./assets/FuturaPTCond-ExtraBold.eot?#iefix") format("embedded-opentype"),
    url("./assets/FuturaPTCond-ExtraBold.woff2") format("woff2"),
    url("./assets/FuturaPTCond-ExtraBold.woff") format("woff"),
    url("./assets/FuturaPTCond-ExtraBold.ttf") format("truetype");
  font-weight: 800;
  font-style: normal;
}

@font-face {
  font-family: "Futura PT";
  src: url("./assets/FuturaPT-MediumObl.eot");
  src: local("Futura PT Medium Oblique"), local("FuturaPT-MediumObl"),
    url("./assets/FuturaPT-MediumObl.eot?#iefix") format("embedded-opentype"),
    url("./assets/FuturaPT-MediumObl.woff2") format("woff2"),
    url("./assets/FuturaPT-MediumObl.woff") format("woff"),
    url("./assets/FuturaPT-MediumObl.ttf") format("truetype");
  font-weight: 500;
  font-style: italic;
}

@font-face {
  font-family: "Futura PT Cond";
  src: url("./assets/FuturaPTCond-Bold.eot");
  src: local("Futura PT Cond Bold"), local("FuturaPTCond-Bold"),
    url("./assets/FuturaPTCond-Bold.eot?#iefix") format("embedded-opentype"),
    url("./assets/FuturaPTCond-Bold.woff2") format("woff2"),
    url("./assets/FuturaPTCond-Bold.woff") format("woff"),
    url("./assets/FuturaPTCond-Bold.ttf") format("truetype");
  font-weight: bold;
  font-style: normal;
}

@font-face {
  font-family: "Futura PT";
  src: url("./assets/FuturaPT-BoldObl.eot");
  src: local("Futura PT Bold Oblique"), local("FuturaPT-BoldObl"),
    url("./assets/FuturaPT-BoldObl.eot?#iefix") format("embedded-opentype"),
    url("./assets/FuturaPT-BoldObl.woff2") format("woff2"),
    url("./assets/FuturaPT-BoldObl.woff") format("woff"),
    url("./assets/FuturaPT-BoldObl.ttf") format("truetype");
  font-weight: bold;
  font-style: italic;
}

@font-face {
  font-family: "Futura PT Book";
  src: url("./assets/FuturaPT-Book.eot");
  src: local("Futura PT Book"), local("FuturaPT-Book"),
    url("./assets/FuturaPT-Book.eot?#iefix") format("embedded-opentype"),
    url("./assets/FuturaPT-Book.woff2") format("woff2"),
    url("./assets/FuturaPT-Book.woff") format("woff"),
    url("./assets/FuturaPT-Book.ttf") format("truetype");
  font-weight: normal;
  font-style: normal;
}

@font-face {
  font-family: "Futura PT";
  src: url("./assets/FuturaPT-Light.eot");
  src: local("Futura PT Light"), local("FuturaPT-Light"),
    url("./assets/FuturaPT-Light.eot?#iefix") format("embedded-opentype"),
    url("./assets/FuturaPT-Light.woff2") format("woff2"),
    url("./assets/FuturaPT-Light.woff") format("woff"),
    url("./assets/FuturaPT-Light.ttf") format("truetype");
  font-weight: 300;
  font-style: normal;
}

@font-face {
  font-family: "Futura PT Cond";
  src: url("./assets/FuturaPTCond-MediumObl.eot");
  src: local("Futura PT Cond Medium Oblique"), local("FuturaPTCond-MediumObl"),
    url("./assets/FuturaPTCond-MediumObl.eot?#iefix") format("embedded-opentype"),
    url("./assets/FuturaPTCond-MediumObl.woff2") format("woff2"),
    url("./assets/FuturaPTCond-MediumObl.woff") format("woff"),
    url("./assets/FuturaPTCond-MediumObl.ttf") format("truetype");
  font-weight: 500;
  font-style: italic;
}

@font-face {
  font-family: "Futura PT Extra";
  src: url("./assets/FuturaPT-ExtraBoldObl.eot");
  src: local("Futura PT Extra Bold Oblique"), local("FuturaPT-ExtraBoldObl"),
    url("./assets/FuturaPT-ExtraBoldObl.eot?#iefix") format("embedded-opentype"),
    url("./assets/FuturaPT-ExtraBoldObl.woff2") format("woff2"),
    url("./assets/FuturaPT-ExtraBoldObl.woff") format("woff"),
    url("./assets/FuturaPT-ExtraBoldObl.ttf") format("truetype");
  font-weight: 800;
  font-style: italic;
}
#app {
  font-family: "Futura PT";
  font-weight: 500;
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
  font-family: "Futura PT";
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
