<template>
  <div class="alpha">

    <div class="header-select">
      <p @click="changeScreen" class="btn">Overview</p>
      <p @click="changeScreen2" class="btn">Logs (1)</p>
      <p @click="changeScreen3" class="btn">State</p>
    </div>

    <div v-show="this.screen === 'crypto'" class="section-1">
      <div class="separate mobile-seprate">
        <div class="inner">
          <i class='bx bx-info-circle'></i>
          <p class="text-1">Rebroadcast Hash:</p>
        </div>
        <div class="inner">
          <p class="text-2">0x1ed4cedfb235556ee5598c902dff761eaa7927b7f869e8b4d04fa1228fb2d9f8</p>
        </div>
      </div>

      <div class="separate">
        <div class="inner">
          <i class='bx bx-info-circle'></i>
          <p class="text-1">Rebroadcast fees :</p>
        </div>
        <div class="inner">
          <p class="text-2 status-3 status-2-mobile">
            <i class='bx bx-check-circle'></i>
            Success
          </p>
        </div>
      </div>

      <div class="separate">
        <div class="inner">
          <i class='bx bx-info-circle'></i>
          <p class="text-1">Proof of stake fee :</p>
        </div>
        <div class="inner">
          <p class="text-2 status-3 status-2-mobile">
            <i class='bx bx-check-circle'></i>
            Success
          </p>
        </div>
      </div>

      <div class="separate">
        <div class="inner">
          <i class='bx bx-info-circle'></i>
          <p class="text-1">Gas fees :</p>
        </div>
        <div class="inner">
          <p class="text-2 status status-2-mobile">
            <i class='bx bx-check-circle'></i>
            Pending
          </p>
        </div>
      </div>

      <div class="separate mobile-seprate">
        <div class="inner">
          <i class='bx bx-info-circle'></i>
          <p class="text-1">Block :</p>
        </div>
        <div class="inner">
          <p class="text-2 status-2-mobile">
            <i style="color: #4BB543" class='bx bx-check-circle'></i> 21647915 <span style="margin-left: 5px;" class="status-2  status-2-mobile">69133 block confirmations.</span>
          </p>
        </div>
      </div>

      <div class="separate">
        <div class="inner">
          <i class='bx bx-info-circle'></i>
          <p class="text-1">TimeStamp :</p>
        </div>
        <div class="inner">
          <p class="text-2">
            <i class='bx bx-time-five' ></i>
            October
          </p>
        </div>
      </div>

      <hr class="line"/>

      <br/>
      <div class="separate mobile-seprate">
        <div class="inner">
          <i class='bx bx-highlight'></i>
          <p class="text-1">Transaction Action :</p>
        </div>
        <div class="inner">
          <p class="text-2">
            Amount $8,000,000 BTC To 0x1ed4cedfb235556ee5598c902dff761eaa7927b7f869e8b4d04fa1228fb2d9f8
          </p>
        </div>
      </div>

    </div>

    <div v-show="this.screen === 'forex'" class="section-1">
      <div class="separate mobile-seprate">
        <div class="inner">
          <i class='bx bx-info-circle'></i>
          <p class="text-1">Address :</p>
        </div>
        <div class="inner">
          <p class="text-2">0x1ed4cedfb235556ee5598c902dff761eaa7927b7f869e8b4d04fa1228fb2d9f8</p>
        </div>
      </div>

      <div class="separate">
        <div class="inner">
          <i class='bx bx-info-circle'></i>
          <p class="text-1">Value :</p>
        </div>
        <div class="inner">
          <p class="text-2">
            $8,000,000 BTC
          </p>
        </div>
      </div>

    </div>

    <div v-show="this.screen === 'stocks'" class="section-1">
      <div class="separate">
        <div class="inner">
          <i class='bx bx-info-circle'></i>
          <p class="text-1">A set of information that represents the current state and amount is updated when a
            transaction takes place on the network. The below is a summary of those changes :</p>
        </div>
<!--        <div class="inner">-->
<!--          <p class="text-2">0x1ed4cedf….fa1228fb2d9f8   $8,000,000</p>-->
<!--        </div>-->
      </div>

      <div class="separate">
        <div class="inner">
          <i class='bx bx-info-circle'></i>
          <p class="text-1">0x1ed4cedf….fa1228fb2d9f8   $8,000,000 </p>
        </div>
<!--        <div class="inner">-->
<!--          <p class="text-2">-->
<!--            $8,000,000 BTC-->
<!--          </p>-->
<!--        </div>-->
      </div>

    </div>


  </div>
</template>


<script>
export default {
  name: "AboutView",
  data() {
    return {
      screen: "crypto",
    };
  },
  methods: {
    changeScreen() {
      this.screen = "crypto"
    },
    changeScreen2() {
      this.screen = "forex"
    },
    changeScreen3() {
      this.screen = "stocks"
    },
  }
}
</script>

<style scoped>

.alpha{
  height: 100%;
  padding-bottom: 3%;
  padding-top: 1%;
}

.header-select{
  display: flex;
  justify-content: center;
  gap: 15px;
  margin-bottom: 1%;
  margin-top: 2%;
}

.btn{
  background-image: linear-gradient(87.71deg, #38ffea 3.28%, #72a2ff 114.54%);
  border: none;
  color: #000000;
  padding: 0.6em 40px 0.5em 40px;
  border-radius: 10px;
  position: relative;
  display: inline-block;
  margin: 0;
  text-decoration: none;
  -webkit-transition: all 0.1s ease;
  transition: all 0.25s ease;
}

.section-1{
  width: 70%;
  margin-left: auto;
  margin-right: auto;
  --tw-bg-opacity: 1;
  background-color: rgb(7 12 20 / var(--tw-bg-opacity));
  padding: 3rem 2.5rem;
  border-radius: 10px;
  box-shadow: rgba(7, 12, 20, 0.2) 0px 2px 8px 0px;
  margin-top: 3%;
}

.separate{
  display: flex;
  gap: 20px;
  align-content: center;
  align-items: center;
  padding-top: 1.5%;
  padding-bottom: 1.5%;
}

.inner{
  display: flex;
  align-content: center;
  align-items: center;
  gap: 5px;
}

.bx-info-circle{
  color: rgb(212 235 255);
}
.bx-highlight{
  color: rgb(212 235 255);
}

.text-1{
  color: rgb(212 235 255);
}

.text-2{
  color: rgb(212 235 255);
  word-wrap: break-word; /* Breaks long words to the next line */
  overflow-wrap: break-word; /* Preferred modern alternative */
  white-space: normal; /* Allows wrapping */
}

.status{
  background-color: #cc0000;
  padding: 7px 18px 4px 18px;
  color: #FFFFFF;
  border-radius: 5px;
  font-size: 14px;
}

.status-2{
  background-color: rgb(211, 211, 211);
  color: #000000;
  padding: 7px 18px 7px 18px;
  border-radius: 5px;
  font-size: 14px;
}

.status-3{
  background-color: #4BB543;
  color: #FFFFFF;
  padding: 7px 18px 4px 18px;
  border-radius: 5px;
  font-size: 14px;
}

.line{
  border: 0.5px solid rgb(212 235 255);
}

@media (max-width: 990px) {

}

@media (max-width: 700px){


  .header-select{
    gap: 5px;
    margin-top: 5%;
    margin-bottom: 5%;
  }

  .btn{
    padding: 0.5em 30px 0.4em 30px;
  }

  .section-1{
    width: 95%;
    margin-top: 5%;
  }

  .mobile-seprate{
    display: block;
  }

  .inner{
    padding-bottom: 10px;
  }

  .text-2{
    width: 100%;
    color: rgb(212 235 255);
    word-wrap: break-word; /* Breaks long words to the next line */
    overflow-wrap: break-word; /* Preferred modern alternative */
    white-space: normal; /* Allows wrapping */
  }

}

@media (max-width: 500px){
  .status-2-mobile {
    font-size: 12px;
  }
}

</style>