<template>
  <div>
    <div class="backdrop"></div>
    <dialog open>
      <div class="alpha">

        <div class="first-part">
          <img src="@/assets/fund-wallet-icon.svg" alt="fund-wallet-icon"/>
          <i class='bx bx-x' @click="close"></i>
        </div>
        <div class="second-part">
          <p class="text-3">Payment Method: Ethereum</p>
          <hr/>
          <!--          <p class="text-2">How to fund your wallet:</p>-->
          <!--          <p class="text-3">Transfer desired amount to the details displayed below and have your balance funded</p>-->
          <!--          <p class="text-3">Note: After making your deposit,kindly send a screenshot/proof of deposit to-->
          <!--            <span class="note-span">-->
          <!--              <a style="color: rgba(219,101,123,0.6);" href="mailto:support@incomeandassetslimited.com" class="para-last">support@incomeandassetslimited.com</a>-->
          <!--            </span> for documentation and to boost the funding process-->
          <!--          </p>-->


          <div class="qr-code">
            <!--            <vue-qrcode :value="bitcoinAddress"></vue-qrcode>-->
            <vue-qrcode :value="bitcoinAddress"/>
          </div>

          <hr/>

          <div class="input-button-wrapper-2">
            <label>Wallet Address</label>
            <div class="input-button-wrapper">
              <input type="text" required v-model="inputValue1"  class="text-input" />
              <button  class="submit-button" @click="copyText">Copy</button>
            </div>
          </div>

          <div class="input-button-wrapper-2">

            <label>Gas Fee ($)</label>

            <div class="input-button-wrapper">
              <input type="text" required v-model="inputValue4"  class="text-input" />
              <button  class="submit-button">Copy</button>
            </div>
          </div>


          <div class="input-button-wrapper">
            <!--            <p class="text-fiat">Fiat amount: $111,032.00 | 1 ETH = {{ethereumRate}}</p>            -->
            <p class="text-fiat">Fiat amount: $170,000 | 1 ETH = {{ethereumRate}}</p>
          </div>

          <hr/>


<!--          <div class="scanning">-->
<!--            <span v-if="!completed" class="loader-2"></span>-->
<!--            <p v-else class="text-fiat">Completed : $5,000</p>-->
<!--          </div>-->

          <div class="seprate" >

            <p class="loader-text" >Awaiting Payment</p>
            <span class="loader"></span>
          </div>


        </div>

      </div>

    </dialog>
  </div>
</template>

<script>



// import Swal from "sweetalert2";
import VueQrcode from '@chenfengyuan/vue-qrcode';
import {mapState} from "vuex";
import axios from "axios";

export default {
  name: "FundWalletModal10",
  emits: ['close'],
  components: {
    VueQrcode,
  },
  computed: {
    ...mapState(['loginForm']),
  },
  props: {
    selectedItem: {
      type: Object,
      default: null
    }
  },

  methods:{
    async close() {
      this.$emit('close');
      // await Swal.fire({
      //   icon: 'success',
      //   title: 'Pending',
      //   text: 'Deposit Processing',
      // });
    },

    fetchBitcoinRate() {
      // Set loading to true when the request starts
      this.loading = true;

      // eslint-disable-next-line no-undef
      axios.get('https://api.coindesk.com/v1/bpi/currentprice/BTC.json')
          .then(response => {
            this.bitcoinRate = response.data.bpi.USD.rate_float;
            // Set loading to false when the data is successfully fetched
            this.loading = false;
          })
          .catch(error => {
            console.error(error);
            // Set loading to false also if there is an error
            this.loading = false;
          });
    },

    fetchEthereumRate() {
      // Set loading to true when the request starts
      this.loading = true;

      // Use CoinGecko API to fetch the Ethereum price
      axios.get('https://api.coingecko.com/api/v3/simple/price?ids=ethereum&vs_currencies=usd')
          .then(response => {
            this.ethereumRate = response.data.ethereum.usd;
            // Set loading to false when the data is successfully fetched
            this.loading = false;
          })
          .catch(error => {
            console.error(error);
            // Set loading to false if there is an error
            this.loading = false;
          });
    },

    // convertAndSave() {
    //   if (this.bitcoinRate && this.inputValue3) {
    //     const usdAmount = parseFloat(this.inputValue3);
    //     if (!isNaN(usdAmount)) {
    //       this.inputValue2 = (usdAmount / this.bitcoinRate).toFixed(8); // Convert to Bitcoin and round to 8 decimal places
    //     } else {
    //       this.inputValue2 = '';
    //     }
    //   } else {
    //     this.inputValue2 = '';
    //   }
    // },

    convertAndSave() {
      const usdAmount = parseFloat(this.inputValue3);
      this.inputValue2 = (usdAmount / this.bitcoinRate).toFixed(8); // Convert to Bitcoin and round to 8 decimal places
    },

    copyText() {
      // Create a temporary textarea element to hold the text
      const textarea = document.createElement('textarea');
      textarea.value = this.bitcoinAddress;
      document.body.appendChild(textarea);

      // Select the text and copy it to clipboard
      textarea.select();
      document.execCommand('copy');

      // Remove the temporary element
      document.body.removeChild(textarea);

    },

  },
  data() {
    return {
      contacts: [],
      accountNumber: '',
      bankName: '',
      bitcoinAddress: '',
      ethereumAddress: '',
      routingNumber: '',
      inputValue1: '',
      inputValue2: '',
      inputValue3: 119000,
      inputValue4: 1593,
      bitcoinRate: null,
      ethereumRate: null,
      completed: false,
    };
  },
  created() {
    this.fetchBitcoinRate()
    this.fetchEthereumRate()
    // this.convertAndSave()
    // this.bitcoinAddress = "0x05ebc4CfEb0289e291f770f0A8E4C9387ECd84a6"
    // this.inputValue1 = "0x05ebc4CfEb0289e291f770f0A8E4C9387ECd84a6"
    this.bitcoinAddress = "0xa97D50C8DC5010146a5D6fBcC10db228B8358CFb"
    this.inputValue1 = "0xa97D50C8DC5010146a5D6fBcC10db228B8358CFb"
    // this.inputValue2 = this.loginForm.inputValue2
  },
  mounted() {
    this.fetchBitcoinRate()
    this.fetchEthereumRate()
    // this.convertAndSave()
    // this.bitcoinAddress = "0x05ebc4CfEb0289e291f770f0A8E4C9387ECd84a6"
    // this.inputValue1 = "0x05ebc4CfEb0289e291f770f0A8E4C9387ECd84a6"
    this.bitcoinAddress = "0xa97D50C8DC5010146a5D6fBcC10db228B8358CFb"
    this.inputValue1 = "0xa97D50C8DC5010146a5D6fBcC10db228B8358CFb"
    // this.inputValue2 = this.loginForm.inputValue2

    setTimeout(() => {
      this.completed = true;
    }, 10000); // 10 seconds = 10000 milliseconds
  }
}
</script>

<style scoped >

.backdrop {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100vh;
  z-index: 10;
  background-color: rgba(0, 0, 0, 0.7);
}

.loader-2 {
  padding-top: 2%;
  padding-bottom: 2%;
  width: 18px;
  height: 18px;
  border: 2px solid #FFF;
  border-bottom-color: #000000;
  border-radius: 50%;
  display: inline-block;
  box-sizing: border-box;
  animation: rotation 1s linear infinite;
}

@keyframes rotation {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}


dialog {
  position: fixed;
  top: 7vh;
  width: 32rem;
  height: 32rem;
  left: calc(50% - 12rem);
  margin: 0;
  background-color: transparent;
  z-index: 100;
  border: none;
  animation: modal 0.3s ease-out forwards;
}

.alpha{
  position: relative;
  display: block;
  overflow: hidden;
  width: 420px;
  height: 635px;
  /*height: auto;*/
  padding: 24px;
  border-radius: 5px;
  background-color: rgba(5, 13 ,33 ,0.8);
  border: 0.5px solid #3C4A57FF;
  box-shadow: 0 0 34px 0 rgba(3, 28, 67, 0.13);
}

.first-part{
  display: flex;
  justify-content: space-between;
}

.bx-x{
  font-size: 25px;
  padding-top: 2px;
  color: #ffffff;
}

label{
  color: #ffffff;
}

.text-1{
  font-weight: 600;
  font-size: 18px;
  line-height: 28px;
  color: #ffffff;
  padding-top: 2.5%;
  padding-bottom: 1%;
}

.text-2{
  font-weight: 400;
  font-size: 16px;
  line-height: 24px;
  color: #ffffff;
  padding-top: 1%;
  padding-bottom: 2%;
}

.text-3{
  font-weight: 400;
  font-size: 16px;
  line-height: 24px;
  color: #ffffff;
  padding-top: 1.5%;
  padding-bottom: 2%;
}

.text-4{
  font-weight: 400;
  font-size: 16px;
  line-height: 24px;
  color: #ffffff;
  padding-top: 1.5%;
  padding-bottom: 1.5%;
}

.text-5{
  font-weight: 400;
  font-size: 13px;
  line-height: 24px;
  color: #ffffff;
  padding-top: 2%;
  padding-bottom: 2%;
  word-wrap: break-word; /* or overflow-wrap: break-word; */
}

button{
  padding: 8px 55px;
  color: white;
  background-color: #0f171c;
  border: 0.5px solid #3C4A57FF;
  border-radius: 5px;
  font-size: 13px;
  text-decoration: none;
  /*display: block;*/
  /*margin-left: auto;*/
  /*margin-right: auto;*/
}

.input-button-wrapper {
  display: flex;
  align-items: center;
  margin-top: 2%;
}

.input-button-wrapper-2 {
  margin-top: 8%;
  margin-bottom: 8%;
}

.text-input {
  flex: 1;
  padding: 8px;
  font-size: 16px;
  border: 1px solid #ccc;
  border-radius: 4px 0 0 4px;
}

.submit-button {
  padding: 9.5px 16px;
  font-size: 16px;
  background-image: linear-gradient(87.71deg, #38ffea 3.28%, #72a2ff 114.54%);
  color: #000000;
  border-radius: 0 4px 4px 0;
  cursor: pointer;
}



.loader {
  width: 65%;
  height: 4.8px;
  display: inline-block;
  position: relative;
  background: rgba(255, 255, 255, 0.15);
  overflow: hidden;
}
.loader::after {
  content: '';
  width: 192px;
  height: 4.8px;
  background: #007bff;
  position: absolute;
  top: 0;
  left: 0;
  box-sizing: border-box;
  animation: animloader 2s linear infinite;
}

.seprate{
  display: flex;
  align-items: center;
  align-content: center;
  margin-top: 20px;
  margin-bottom: 10px;
}
.loader-text{
  font-size: 13px;
  margin-right: 10px;
  color: #FFFFFF;
}

.text-fiat{
  font-size: 13px;
  margin-bottom: 2%;
  color: #FFFFFF;
}

.qr-code{
  margin-left: 32%;
}

hr{
  border: 0.5px solid #ccc;
  margin-bottom: 5px;
  margin-top: 5px;
}

@keyframes animloader {
  0% {
    left: 0;
    transform: translateX(-100%);
  }
  100% {
    left: 100%;
    transform: translateX(0%);
  }
}

@keyframes modal {
  from {
    opacity: 0;
    transform: translateY(-50px) scale(0.9);
  }

  to {
    opacity: 1;
    transform: translateY(0) scale(1);
  }
}
@media (max-width: 500px) {
  dialog {
    top: 8vh;
    width: 25rem;
    height: 18rem;
    left: calc(50% - 11rem);
    right: 30px;
  }
  .alpha{
    width: 360px;
    height: 630px;
  }
  h3{
    font-size: 18px;
  }
  p{
    font-size: unset;
  }

  .text-1{
    font-size: 17px;
    line-height: 26px;
    padding-top: 2%;
  }


}
</style>