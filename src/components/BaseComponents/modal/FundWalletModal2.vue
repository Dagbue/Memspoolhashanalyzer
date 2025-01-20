<template>
  <div>
    <div class="backdrop"></div>
    <dialog open>
      <div class="alpha">

        <div class="first-part">
<!--          <img src="@/assets/fund-wallet-icon.svg" alt="fund-wallet-icon"/>-->
          <i class='bx bx-x'  @click="close"></i>
        </div>


<!--        <img src="@/assets/modal.png" alt="modal.png" class="modalimage" loading="lazy" />-->

        <picture>
          <source srcset="@/assets/modal.webp" type="image/webp">
          <img src="@/assets/modal.png" alt="modal.png" class="modalimage" loading="lazy" />
        </picture>


      </div>

    </dialog>
  </div>
</template>

<script>
// import Swal from "sweetalert2";

export default {
  name: "FundWalletModal2",
  emits: ['close'],
  props: {
    selectedItem: {
      type: Object,
      default: null
    }
  },
  computed:{

  },
  methods:{
    async close() {
      this.$emit('close');
      // await Swal.fire({
      //   icon: 'success',
      //   title: 'Pending',
      //   text: 'Loan Request Pending',
      // });
    },
  },
  data() {
    return {

    };
  },
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
  left: calc(50% - 16rem);
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
  width: 500px;
  height: 550px;
  /*height: auto;*/
  padding: 24px;
  border-radius: 5px;
  background-color: transparent;
}

.first-part{
  display: flex;
  justify-content: space-between;
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
}

.text-2{
  font-weight: 400;
  font-size: 16px;
  line-height: 24px;
  color: #070e20;
  padding-top: 1%;
  padding-bottom: 2%;
}

.text-3{
  font-weight: 400;
  font-size: 16px;
  line-height: 24px;
  color: #070e20;
  padding-top: 1.5%;
  padding-bottom: 2%;
}

.text-4{
  font-weight: 400;
  font-size: 16px;
  line-height: 24px;
  color: #070e20;
  padding-top: 1.5%;
  padding-bottom: 1.5%;
}

.text-5{
  font-weight: 400;
  font-size: 13px;
  line-height: 24px;
  color: #070e20;
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
  margin-bottom: 8%;
  margin-top: 8%;
}

.text-input {
  flex: 1;
  padding: 8px;
  font-size: 16px;
  border: 1px solid #ccc;
  border-radius: 4px 0 0 4px;
}

.submit-button {
  padding: 8px 16px;
  font-size: 16px;
  background-color: #007bff;
  color: white;
  border: 1px solid #007bff;
  border-radius: 0 4px 4px 0;
  cursor: pointer;
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
}

.modalimage {
  width: 100%;
}

.bx-x{
  display: flex;
  justify-content: right;
  float: right;
  color: #ffffff;
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