<template>
  <div id="app">

    <div class='container footer-signup'>
  <div class='inside'>
    <h2>
      {{ error }}
    </h2>
    <form id='signup_form'>

      <fieldset id='firstField'>
        <p>
          <input id='signup_name' v-model="name" placeholder="Name" name='name' type='text' value=''>
        </p>
        <p>
          <input id='signup_email' v-model="email" placeholder="Email" name='email' type='text' value=''>
        </p>
        <p>
           <vue-recaptcha
            style="width: none; height: none; background:none !important"
            theme ='light'
            :sitekey="siteKey"
            @verify="verifyMethod"
            class="recaptcha"
          >
          </vue-recaptcha>
        </p>
        <p class='button'>
          <input id='newsletter' name='' type='button' value='Submit' :disabled="!verified" @click="submitReg">
        </p>
      </fieldset>
    </form>

  </div>
</div>


    <div class="wrapper" style="display:none">
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

.rc-anchor-normal {
    height: none !important;
     width: none !important;
}

.rc-anchor-light.rc-anchor-normal {
    border: 0px solid #d3d3d3 !important;
}

.rc-anchor-light {
    background:none !important;
    color: #000;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  margin-top: 60px;
}

/* .row {
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
} */

html, body, div, span, applet, object, iframe, h1, h2, h3, h4, h5, h6, p, blockquote, pre, a, abbr, acronym, address, big, cite, code, del, dfn, em, img, ins, kbd, q, s, samp, small, strike, strong, sub, sup, tt, var, b, u, i, center, dl, dt, dd, ol, ul, li, fieldset, form, label, legend, table, caption, tbody, tfoot, thead, tr, th, td, article, aside, canvas, details, embed, figure, figcaption, footer, header, hgroup, menu, nav, output, ruby, section, summary, time, mark, audio, video {
    margin: 0;
    padding: 0;
    border: 0;
    font: inherit;
    font-size: 100%;
    vertical-align: baseline
}
html {
    line-height: 1
}
ol, ul {
    list-style: none
}
table {
    border-collapse: collapse;
    border-spacing: 0
}
caption, th, td {
    text-align: left;
    font-weight: normal;
    vertical-align: middle
}
q, blockquote {
    quotes: none
}
q:before, q:after, blockquote:before, blockquote:after {
    content: "";
    content: none
}
a img {
    border: none
}
article, aside, details, figcaption, figure, footer, header, hgroup, menu, nav, section, summary {
    display: block
}
* {
    -webkit-box-sizing: border-box;
    -moz-box-sizing: border-box;
    box-sizing: border-box
}
body {
    background: #fff;
    font-weight: 400;
    font-size: 100%;
    line-height: 1.5em;
    font-family: "Open Sans", "open-sans", sans-serif;
    -webkit-font-smoothing: antialiased;
    color: rgb(255, 255, 255)
}
p {
    font-size: 18px;
    line-height: 1.8em;
    color: #333
}
a, button, input, textarea, select {
    outline: none
}
a {
    display: inline-block;
    text-decoration: none;
    color: #F26E00
}
input, textarea, button {
    -webkit-appearance: none;
    border-radius: 0;
    outline: none;
    resize: none;
    font-family: "Open Sans", "open-sans", sans-serif;
    -webkit-font-smoothing: antialiased
}
strong {
    font-weight: 700
}
img {
    display: inline-block
}
iframe {
    position: relative;
    z-index: 15
}
h1, h2, h3, h4, h5 {
    font-family: "brandon-grotesque", sans-serif
}
h1 {
    font: 300 45px/65px "Open Sans", "open-sans", sans-serif;
    margin-bottom: 75px;
    color: #323a45
}
h2 {
    font: 300 35px/52px "Open Sans", "open-sans", sans-serif;
    color: #323a45;
    margin-bottom: 30px
}
h3 {
    font: 700 40px/1.5em "brandon-grotesque", sans-serif;
    color: #323a45;
    text-transform: uppercase;
    margin-bottom: 18px
}
h4 {
    font: 600 13px/1.2em "Open Sans", "open-sans", sans-serif;
    color: #323a45
}

/***********************************************************************************************/
.container {
    background-color: #fff;
    padding: 100px 0;
    position: relative
}
.container.alt {
    background-color: #f9f9fa
}
.container.dark h1, .container.dark h2, .container.dark h3, .container.dark h4, .container.dark h5 {
    color: #fff
}
.container.dark-blue {
    background: #323a45
}
.container.dark-blue h1, .container.dark-blue h2, .container.dark-blue h3, .container.dark-blue h4, .container.dark-blue h5 {
    color: #fff
}
.container .inside {
    *zoom: 1;
    max-width: 1320px;
    margin-left: auto;
    margin-right: auto;
    padding: 0 20px;
    clear: both;
}
.container .inside:before, .container .inside:after {
    content: " ";
    display: table;
}
.container .inside:after {
    clear: both;
}

.clearfix {*zoom: 1;clear: both;}
.clearfix:before, .clearfix:after {
    content: " ";
    display: table;
}
.clearfix:after {
    clear: both;
}

.hidden {
  display: none;
}
/* ********************************************************************************************* */

.inline-block {
    display: inline-block;
    *display: inline;
    *zoom: 1
}
button {
    margin: 0px;
    padding: 0px;
    border: 0px;
    font-weight: normal
}
p.button a,
p.button input,
p.button button {
    display: inline-block;
    padding: 20px 80px;
    background: #F26E00;
    border: 0;
    border-radius: 0;
    color: #fff;
    font-size: 19px;
    line-height: 1em;
    font-family: "Open Sans", sans-serif;
    font-weight: 400;
    cursor: pointer;
    -webkit-transition: background 0.3s false;
    -moz-transition: background 0.3s false false;
    -o-transition: background 0.3s false false;
    transition: background 0.3s
}
p.button a:hover,
p.button input:hover,
p.button button:hover {
    background: #F26E00;
}
p.button input {
    padding: 23px 40px 22px;
}
form {
    display: inline-block;
    margin-bottom: 20px;
}
form p {
    position: relative;
    float: left;
    margin: 0;
}
form input, form textarea {
    font: 400 18px/1em "Open Sans", "open-sans", sans-serif;
    color: #8a959e;
}
form input.error, form textarea.error {
    border-color: #f36;
    box-shadow: 0 0 0 1px #f36;
}
form textarea {
    overflow: auto;
}
form label {
    position: absolute;
    top: 0;
    left: 0;
    font-size: 18px;
    color: #a2a2a2;
    margin: 15px 0px;
    font-weight: 400;
}
form label.error {
    display: none !important;
}
form input[type=text],
form input[type=search],
form input[type=email],
form input[type=password],
form textarea {
    background: #fff;
    width: 232px;
    line-height: 1em;
    -webkit-border-radius: 0;
    -moz-border-radius: 0;
    -ms-border-radius: 0;
    -o-border-radius: 0;
    border-radius: 0;
    padding: 18px 15px;
    margin-right: 10px;
    border: 1px solid #d4d7da
}
form input[type=text].error,
form input[type=search].error,
form input[type=email].error,
form input[type=password].error,
form textarea.error {
    border-color: #f36
}
#signup_form .group {
  margin-bottom: 10px
}
.footer-signup {
  text-align: center;
  padding: 6px 0 45px
}
.footer-signup h2 {
  font-size: 20px
}
.footer-signup p i {
  position: absolute;
  top: 22px;
  left: 15px;
  color: #a2a2a2;
}
.footer-signup p label {
    margin-left: 50px
}
.footer-signup p input[type=text], .footer-signup p input[type=password] {
    width: 280px;
    height: 50px;
    padding-left: 20px;
    border:none;
    border-right: 1px solid gray;
}
@media (max-width: 1145px) {
    .footer-signup p input[type=text], .footer-signup p input[type=password] {
        width: 240px
    }
}
.footer-signup p.button input {
    padding: 15px 60px;
    height: 50px;
    line-height: 0.8em;
    border-radius: 6px;
}
.footer-signup p.terms {
    font-size: 12px;
    color: #adafb2
}
.footer-signup p.terms a {
    color: #adafb2;
    text-decoration: underline
}
.footer-signup p.terms a:hover {
    color: #fff
}
.footer-signup p.trust {
    margin-top: 100px;
    color: #8a959e;
    font: 300 italic 22px/1em "Open Sans", "open-sans", sans-serif
}
.footer-signup ul {
    display: block;
    max-width: 984px;
    margin: 0px auto;
    padding-top: 48px
}
.footer-signup li {
    display: inline-block;
    vertical-align: middle
}
.footer-signup li.stretch {
    width: 100%;
    font-size: 0;
    line-height: 0
}
.footer-signup li a {
    vertical-align: bottom;
    overflow: hidden;
    text-indent: 9000px;
    text-transform: capitalize
}
.footer-signup .adobe a {
    display: inline-block;
    /* background-image: url('../img/sprites/global-s378a0102c0.png'); */
    background-position: 0 -1287px;
    background-repeat: no-repeat;
    height: 23px;
    width: 99px
}
@media (-webkit-min-device-pixel-ratio: 1.5), (min--moz-device-pixel-ratio: 1.5), (-o-min-device-pixel-ratio: 3 / 2), (min-device-pixel-ratio: 1.5), (min-resolution: 144dpi) {
    .footer-signup .adobe a {
        /* background-image: url('../img/sprites-retina/global-s70aaad24ad.png'); */
        -webkit-background-size: 141px auto;
        -moz-background-size: 141px auto;
        -o-background-size: 141px auto;
        background-size: 141px auto;
        background-position: 0 -804px
    }
}
.footer-signup .ebay a {
    display: inline-block;
    /* background-image: url('../img/sprites/global-s378a0102c0.png'); */
    background-position: 0 -1021px;
    background-repeat: no-repeat;
    height: 33px;
    width: 88px
}
@media (-webkit-min-device-pixel-ratio: 1.5), (min--moz-device-pixel-ratio: 1.5), (-o-min-device-pixel-ratio: 3 / 2), (min-device-pixel-ratio: 1.5), (min-resolution: 144dpi) {
    .footer-signup .ebay a {
        /* background-image: url('../img/sprites-retina/global-s70aaad24ad.png'); */
        -webkit-background-size: 141px auto;
        -moz-background-size: 141px auto;
        -o-background-size: 141px auto;
        background-size: 141px auto;
        background-position: 0 -671px
    }
}
.footer-signup .zappos a {
    display: inline-block;
    /* background-image: url('../img/sprites/global-s378a0102c0.png'); */
    background-position: 0 -484px;
    background-repeat: no-repeat;
    height: 37px;
    width: 97px
}
@media (-webkit-min-device-pixel-ratio: 1.5), (min--moz-device-pixel-ratio: 1.5), (-o-min-device-pixel-ratio: 3 / 2), (min-device-pixel-ratio: 1.5), (min-resolution: 144dpi) {
    .footer-signup .zappos a {
        /* background-image: url('../img/sprites-retina/global-s70aaad24ad.png'); */
        -webkit-background-size: 141px auto;
        -moz-background-size: 141px auto;
        -o-background-size: 141px auto;
        background-size: 141px auto;
        background-position: 0 -134px
    }
}
.footer-signup .shopify a {
    display: inline-block;
    /* background-image: url('../img/sprites/global-s378a0102c0.png'); */
    background-position: 0 -621px;
    background-repeat: no-repeat;
    height: 35px;
    width: 124px
}
@media (-webkit-min-device-pixel-ratio: 1.5), (min--moz-device-pixel-ratio: 1.5), (-o-min-device-pixel-ratio: 3 / 2), (min-device-pixel-ratio: 1.5), (min-resolution: 144dpi) {
    .footer-signup .shopify a {
        /* background-image: url('../img/sprites-retina/global-s70aaad24ad.png'); */
        -webkit-background-size: 141px auto;
        -moz-background-size: 141px auto;
        -o-background-size: 141px auto;
        background-size: 141px auto;
        background-position: 0 -271px
    }
}
.footer-signup .evernote a {
    display: inline-block;
    /* background-image: url('../img/sprites/global-s378a0102c0.png'); */
    background-position: 0 -756px;
    background-repeat: no-repeat;
    height: 36px;
    width: 141px
}
@media (-webkit-min-device-pixel-ratio: 1.5), (min--moz-device-pixel-ratio: 1.5), (-o-min-device-pixel-ratio: 3 / 2), (min-device-pixel-ratio: 1.5), (min-resolution: 144dpi) {
    .footer-signup .evernote a {
        /* background-image: url('../img/sprites-retina/global-s70aaad24ad.png'); */
        -webkit-background-size: 141px auto;
        -moz-background-size: 141px auto;
        -o-background-size: 141px auto;
        background-size: 141px auto;
        background-position: 0 -406px
    }
}
.footer-signup .box a {
    display: inline-block;
    /* background-image: url('../img/sprites/global-s378a0102c0.png'); */
    background-position: 0 -1697px;
    background-repeat: no-repeat;
    height: 32px;
    width: 56px
}
@media (-webkit-min-device-pixel-ratio: 1.5), (min--moz-device-pixel-ratio: 1.5), (-o-min-device-pixel-ratio: 3 / 2), (min-device-pixel-ratio: 1.5), (min-resolution: 144dpi) {
    .footer-signup .box a {
        /* background-image: url('../img/sprites-retina/global-s70aaad24ad.png'); */
        -webkit-background-size: 141px auto;
        -moz-background-size: 141px auto;
        -o-background-size: 141px auto;
        background-size: 141px auto;
        background-position: 0 -1214px
    }
}
.footer-signup .zendesk a {
    display: inline-block;
    /* background-image: url('../img/sprites/global-s378a0102c0.png'); */
    background-position: 0 -350px;
    background-repeat: no-repeat;
    height: 34px;
    width: 133px
}
@media (-webkit-min-device-pixel-ratio: 1.5), (min--moz-device-pixel-ratio: 1.5), (-o-min-device-pixel-ratio: 3 / 2), (min-device-pixel-ratio: 1.5), (min-resolution: 144dpi) {
    .footer-signup .zendesk a {
        /* background-image: url('../img/sprites-retina/global-s70aaad24ad.png'); */
        -webkit-background-size: 141px auto;
        -moz-background-size: 141px auto;
        -o-background-size: 141px auto;
        background-size: 141px auto;
        background-position: 0 0
    }
}


@media (max-width: 1024px) {
    #signup_form {
        display: block
    }
    #signup_form p {
        display: block;
        float: none;
        margin-bottom: 15px
    }
    #signup_form p label {
        left: 50%;
        margin-left: -25%
    }
    #signup_form p i {
        left: 50%;
        margin-left: -29%
    }
    #signup_form p input {
        width: 60%;
        margin: 0px
    }
    .footer-signup ul {
        text-align: center
    }
    .footer-signup ul li {
        margin: 20px
    }
    .footer-signup ul li.stretch {
        display: none
    }
}



@media (max-width: 640px) {

    #signup_form p label {
        left: 50px;
        margin-left: 0px
    }
    #signup_form p i {
        left: 15px;
        margin-left: 0px
    }
    #signup_form p input {
        width: 100%
    }
}
@media (max-width: 490px) {
    .single .invision-share-banner a span {
        display: none
    }
    .single .invision-share-banner p.b-title {
        font-size: 25px
    }
}
@media (max-width: 490px) {
    .single .invision-share-banner {
        padding: 15px 0 0 10px
    }
    .single .invision-share-banner p.b-sub {
        line-height: 23px
    }
    .single .invision-share-banner a {
        margin: 15px 0 0 18px
    }
}

@media only screen and (min-device-width: 320px) and (max-device-width: 568px) and (orientation: landscape) and (-webkit-min-device-pixel-ratio: 1.5), only screen and (min-device-width: 320px) and (max-device-width: 568px) and (orientation: landscape) and (min--moz-device-pixel-ratio: 1.5), only screen and (min-device-width: 320px) and (max-device-width: 568px) and (orientation: landscape) and (-o-min-device-pixel-ratio: 3 / 2), only screen and (min-device-width: 320px) and (max-device-width: 568px) and (orientation: landscape) and (min-device-pixel-ratio: 1.5), only screen and (min-device-width: 320px) and (max-device-width: 568px) and (orientation: landscape) and (min-resolution: 144dpi) {
    body.fixed-nav #main-nav-wrapper.container nav>a {
        /* background-image: url('../img/sprites-retina/global-s70aaad24ad.png'); */
        -webkit-background-size: 141px auto;
        -moz-background-size: 141px auto;
        -o-background-size: 141px auto;
        background-size: 141px auto;
        background-position: 0 -2004px
    }
}
@media only screen and (min-device-width: 320px) and (max-device-width: 568px) and (orientation: landscape) and (-webkit-min-device-pixel-ratio: 1.5), only screen and (min-device-width: 320px) and (max-device-width: 568px) and (orientation: landscape) and (min--moz-device-pixel-ratio: 1.5), only screen and (min-device-width: 320px) and (max-device-width: 568px) and (orientation: landscape) and (-o-min-device-pixel-ratio: 3 / 2), only screen and (min-device-width: 320px) and (max-device-width: 568px) and (orientation: landscape) and (min-device-pixel-ratio: 1.5), only screen and (min-device-width: 320px) and (max-device-width: 568px) and (orientation: landscape) and (min-resolution: 144dpi) {
    body.fixed-nav #main-nav-wrapper.container .inv-menu {
        /* background-image: url('../img/sprites-retina/global-s70aaad24ad.png'); */
        -webkit-background-size: 141px auto;
        -moz-background-size: 141px auto;
        -o-background-size: 141px auto;
        background-size: 141px auto;
        background-position: 0 -3210px
    }
}


</style>
