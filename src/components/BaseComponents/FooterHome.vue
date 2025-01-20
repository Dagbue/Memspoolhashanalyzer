<template>
  <div class="alpha">
    <div class="the-footer">


      <div class="bottom">
        <div class="logo-container">

          <div class="footer-link-container">
            <h3 class="footer-title">❤ Donate BTC: bc1qney2huan0ewtjj0jk8zu7fprnd7yyl0f04mrxe</h3>
            <p style="color: #007bff" class="footer-link">
              Terms & Conditions
            </p>

            <div class="socials-container">
              <img class="social-img" src="https://bitaccelerate.com/media/x_logo.svg" alt="" />
              <img class="social-img" src="https://bitaccelerate.com/media/fb_logo.svg" alt="" />
              <img class="social-img" src="https://bitaccelerate.com/media/yt_logo.svg" alt="" />
              <img class="social-img" src="https://bitaccelerate.com/media/linkedin_logo.svg" alt="" />
              <img class="social-img" src="https://bitaccelerate.com/media/instagram_logo.svg" alt="" />
              <img class="social-img" src="https://bitaccelerate.com/media/pinterest_logo.svg" alt="" />
            </div>

          </div>

        </div>
      </div>
    </div>
  </div>
</template>

<script>

// import BitcoinPrices from "@/components/baseComponents/bitcoinPrices.vue";

export default {
  name: 'FooterHome',
  // components: {BitcoinPrices},
  methods: {
    onPostClick() {
      this.$router.push("/");
      window.scrollTo(0, 0);
    },
    onPostClick2() {
      this.$router.push("/login");
      window.scrollTo(0, 0);
    },
    onPostClick3() {
      this.$router.push("/register");
      window.scrollTo(0, 0);
    },
    onPostClick4() {
      this.$router.push("/faq");
      window.scrollTo(0, 0);
    },
    onPostClick5() {
      this.$router.push("/contact");
      window.scrollTo(0, 0);
    },
  },
  mounted() {
    let externalScript = document.createElement('script')
    externalScript.setAttribute('src', "https://www.livecoinwatch.com/static/lcw-widget.js")
    document.head.appendChild(externalScript)
  },
}
</script>

<style scoped>
.contain{
  width: 90%;
}
.the-footer {
  background-color: #e9ecef;
  color: #070e20;
  padding: 1.5vh  1vh;
  margin-top: 3%;
}

.logo-container {
  display: flex;
  justify-content: center;
  margin-left: 5%;
  /*margin-right: 7%;*/
  padding-top: 1%;
}

.footer-title {
  font-size: 16px;
  line-height: 20px;
  text-align: center;
}

.footer-link {
  display: block;
  font-size: 16px;
  line-height: 25px;
  padding-top: 10px;
  text-align: center;
}

.bottom{
  margin-top: 0.4%;
  margin-bottom: 0.4%;
}

.footer-link-container {
  /*margin-left: 5%;*/
  /*margin-right: 5%;*/
  width: 65%;
}

.footer-link-container2{
  /*padding-right: 5%;*/
}
.stay-connected{

}
.socials-container {
  display: flex;
  justify-content: center;
  width: 100%;
  margin-top: 5px;
}

hr {
  color: #070e20;
  width: 100%;
  background-color: #070e20;
  border: 0.5px solid #070e20;
  opacity: 0.2;
  margin-top: 10px;
  margin-bottom: 10px;
}

.copyright {
  font-size: 13px;
  line-height: 19px;
  margin-top: 5px;
  padding-bottom: 0;
  margin-bottom: 0;
  color: #070e20;
  font-weight: 900;
  text-align: center;
}
.footer-img {
  width: 22%;
}
a {
  text-decoration: none;
  color: #070e20;
  transition: ease 0.3s;
}
a:hover{
  color: #070e20;
  font-weight: 700;
}

.bit{
  margin-bottom: 25px;
}
.bx {
  font-size: 27px;
}
.bx-mail-send{
}
.last-div{
  display: flex;
  margin-bottom: 15px;
}
.last-div-para{
  font-size: 15px;
  padding-left: 10px;
  line-height: 1.3;
  color: #070e20;
}
.footer-title{
  color: #070e20;
  /*font-size: 30px;*/
  font-weight: bold;
}

.google{
  width: 40%;
  margin-left: 2%;
  margin-top: 3%;
}

.social-part-1 i {
  padding-right: 10px;
  margin-top: 1%;
}

img{
  width: 85%;
  padding-right: 20px;
}

a{
  width: 100%;
}

.section-part{
  display: flex;
  justify-content: center;
  align-items: center;
  align-content: center;
  padding-top: 30px;
  padding-bottom: 15px;
  padding-left: 2%;
  /*background: #393939;*/
  margin-top: 2%;
  margin-bottom: 1.5%;
}

.social-img{
  width: 38px;
}


@media (max-width: 990px) {
  .footer-link-container {
    margin-left: auto;
    margin-right: auto;
    width: 100%;
    margin-top: 3%;
  }
}
@media (max-width: 760px) {
  .bottom {
    display: block;
    align-content: center;
    text-align: center;
  }
  .footer-container {
    display: block;
    align-content: center;
    text-align: center;
  }
  .the-footer {
    margin-top: unset;
  }
  .footer-img {
    width: 50%;
    min-width: unset;
    border-radius: 20px;
    margin-bottom: 20px;
  }
  .footer-link-container2 {
    margin-bottom: 10%;
    margin-top: 10%;
  }
  .last-div{
    margin-right: 10%;
    margin-bottom: unset;
  }
  .copyright{
    font-size: 17px;
  }
}
@media (max-width: 700px) {
  .last-div-para{
    text-align: left;
  }
  img{
    width: 100%;
    padding-bottom: 6%;
    padding-right: 20px;
  }
  h1{
    font-size: 25px;
  }
  .footer-link {
    display: block;
    font-size: 16px;
  }
  .footer-title {
    font-size: 15px;
    padding-bottom: unset;
    margin-left: 20px;
    margin-right: 20px;
  }

  .footer-img {
    width: 50%;
    display: block;
    margin-right: auto;
    margin-left: auto;
  }
  .copyright {
    font-size: 13px;
    opacity: 0.8;
    width: 90%;
  }
  .bx{
    font-size: 25px;
  }
  .last-div-para{
    font-size: 16px;
    padding-left: 8px;
  }
  .logo-container {
    display: flex;
    flex-direction: column;
    padding-top: 2%;
  }
  .google{
    width: 45%;
  }

}
@media (max-width: 500px) {
  .copyright{
    font-size: 12px;
  }
  img{
    width: 42%;
    display: block;
    margin-right: auto;
    margin-left: auto;
    padding-bottom: 6%;
  }

  .section-part{
    display: flex;
    justify-content: center;
    flex-direction: column;
    margin-left: unset;
    padding-bottom: 5px;
  }


  .logo-container {
    margin-left: unset;
  }
}
</style>