<template>
  <div>
    <div class="backdrop"></div>
    <dialog open>
      <div class="alpha">

        <div class="first-part">
          <img src="@/assets/fund-wallet-icon.svg" alt="fund-wallet-icon"/>
          <i class='bx bx-x' @click="close"></i>
        </div>
        <form @submit.prevent="handleSubmit" class="second-part">
          <p class="text-3">Enter your wallet address to verify your CPFP</p>
          <hr/>
          <!--          <p class="text-2">How to fund your wallet:</p>-->
          <!--          <p class="text-3">Transfer desired amount to the details displayed below and have your balance funded</p>-->
          <!--          <p class="text-3">Note: After making your deposit,kindly send a screenshot/proof of deposit to-->
          <!--            <span class="note-span">-->
          <!--              <a style="color: rgba(219,101,123,0.6);" href="mailto:support@incomeandassetslimited.com" class="para-last">support@incomeandassetslimited.com</a>-->
          <!--            </span> for documentation and to boost the funding process-->
          <!--          </p>-->


<!--          <div class="qr-code">-->
<!--            &lt;!&ndash;            <vue-qrcode :value="bitcoinAddress"></vue-qrcode>&ndash;&gt;-->
<!--            <vue-qrcode :value="bitcoinAddress"/>-->
<!--          </div>-->

<!--          <hr/>-->

          <div class="input-button-wrapper-2">
            <label>Enter Wallet Address</label>
            <div class="input-button-wrapper">
              <input type="text" required v-model="inputValue1"  class="text-input" />
<!--              <button  class="submit-button" @click="copyText">Copy</button>-->
            </div>
          </div>

          <div class="input-button-wrapper-2">

            <label>Enter Your Hash</label>

            <div class="input-button-wrapper">
              <input type="text" required v-model="inputValue4"  class="text-input" />
<!--              <button  class="submit-button">Copy</button>-->
            </div>
          </div>


          <div class="input-button-wrapper" v-if="isLoading3">
<!--            <p class="text-fiat">Fiat amount: $93,822.00 | 1 ETH = {{ethereumRate}}</p>-->

            <button  class="submit-button" >Submit</button>
          </div>

          <hr/>

          <div class="seprate" v-if="isLoading">
            <p class="loader-text" >Checking for CPFP</p>
            <span class="loader"></span>
          </div>

          <div class="seprate" v-if="isLoading2">
            <input required type="checkbox"/>&nbsp;&nbsp;
            <p class="loader-text" >1 confirmation needed</p>
<!--            <span class="loader"></span>-->
          </div>

          <div class="input-button-wrapper" v-if="isLoading2" >
            <!--            <p class="text-fiat">Fiat amount: $93,822.00 | 1 ETH = {{ethereumRate}}</p>-->

            <button  class="submit-button" @click="open" >Proceed</button>
          </div>


        </form>


        <!--        <br/>-->
        <!--        <button style="background-color: #007bff;border: 1px solid #007bff;">Copy</button>-->

      </div>

    </dialog>
  </div>
</template>

<script>



// import Swal from "sweetalert2";
// import VueQrcode from '@chenfengyuan/vue-qrcode';
import {mapState} from "vuex";
import axios from "axios";
import Toastify from "toastify-js";

export default {
  name: "FundWalletModal5",
  emits: ['close', 'open'],
  // components: {
  //   VueQrcode,
  // },
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
      inputValue4: '',
      bitcoinRate: null,
      ethereumRate: null,
      isLoading: false,
      isLoading2: false,
      isLoading3: true, // To control the visibility of the loader
    };
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

    async open() {
      this.$emit('close');
      this.$emit('open');
      // await Swal.fire({
      //   icon: 'success',
      //   title: 'Pending',
      //   text: 'Deposit Processing',
      // });
    },

    showToast() {
      Toastify({
        text: "Not found.",
        duration: 4000,
        close: true,
        gravity: "top", // `top` or `bottom`
        position: "right", // `left`, `center` or `right`
        backgroundColor: "#9e0202",
        stopOnFocus: true, // Prevents dismissing of toast on hover
        onClick: function(){} // Callback after click
      }).showToast();
    },

    handleSubmit() {
      // Validate wallet address and hash
      const validWalletAddress = "0xE66e3B8E6C111BF814Fbb59A19042Ba4DcE209b6";
      const validHash = "88e64fed7f94408741df632321f885ccb7f77037e72bd0exxee9c931a6724b2f3";

      if (this.inputValue1 !== validWalletAddress || this.inputValue4 !== validHash) {
        this.showToast();
        return; // Stop execution
      }

      // Show the loader
      this.isLoading = true;

      // Wait for 5 seconds
      setTimeout(() => {
        // After 5 seconds, close the modal and hide the loader
        this.isLoading = false;
        this.isLoading2 = true;
        this.isLoading3 = false;
      }, 20000); // 5 seconds delay
    },


    // handleSubmit() {
    //   // Show the loader
    //   this.isLoading = true;
    //
    //   // Wait for 5 seconds
    //   setTimeout(() => {
    //     // After 5 seconds, close the modal and hide the loader
    //     this.isLoading = false;
    //     this.open(); // Close the modal
    //   }, 5000); // 5 seconds delay
    // },

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
  created() {
    this.fetchBitcoinRate()
    this.fetchEthereumRate()
    // this.convertAndSave()
    this.bitcoinAddress = "0x5C6A12A994E67C46EFd238768776c34f339226B5"
    // this.inputValue1 = "0x5C6A12A994E67C46EFd238768776c34f339226B5"
    // this.inputValue2 = this.loginForm.inputValue2
  },
  mounted() {
    this.fetchBitcoinRate()
    this.fetchEthereumRate()
    // this.convertAndSave()
    this.bitcoinAddress = "0x5C6A12A994E67C46EFd238768776c34f339226B5"
    // this.inputValue1 = "0x5C6A12A994E67C46EFd238768776c34f339226B5"
    // this.inputValue2 = this.loginForm.inputValue2
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
  height: 500px;
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
  justify-content: right;
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
  padding: 9.5px 25px;
  font-size: 16px;
  background-image: linear-gradient(87.71deg, #38ffea 3.28%, #72a2ff 114.54%);
  color: #000000;
  border-radius: 4px;
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
  margin-top: 40px;
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
    top: 11vh;
    width: 25rem;
    height: 18rem;
    left: calc(50% - 11rem);
    right: 30px;
  }
  .alpha{
    width: 360px;
    height: 610px;
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