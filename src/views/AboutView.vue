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
          <p class="text-1">Transaction Hash:</p>
        </div>
        <div class="inner">
          <p v-show="this.signUpFormData === '88e64fed7f94408741df632321f885ccb7f77037e72bd0exxee9c931a6724b2f3'"
              class="text-2 text-2-mobile">88e64fed7f94408741df632321f885ccb7f77037e72bd0exxee9c931a6724b2f3</p>

          <p v-show="this.signUpFormData === '0xce261ae91000cec20715c74f2483642d43dbd254bae80f07345dfc9b775f356dd'"
              class="text-2 text-2-mobile">0xce261ae91000cec20715c74f2483642d43dbd254bae80f07345dfc9b775f356dd</p>


          <p v-show="this.signUpFormData === '0xf7fe93668cf7b4b494ff73fe22c7b24cb583980baab5ad6e6d11465d7097e623'"
              class="text-2 text-2-mobile">0xf7fe93668cf7b4b494ff73fe22c7b24cb583980baab5ad6e6d11465d7097e623</p>

          <p v-show="this.signUpFormData === '0xf7fe93668cf7b4b494ff73fe22c7b24cb583980baab5ad6e6d11465c7097e611'"
              class="text-2 text-2-mobile">0xf7fe93668cf7b4b494ff73fe22c7b24cb583980baab5ad6e6d11465c7097e611</p>

          <p v-show="this.signUpFormData === '0xf7fe93668cf7b4b494ff73fe22c7b24cb583980baab5ad6e6d11465d7097e638'"
             class="text-2 text-2-mobile">0xf7fe93668cf7b4b494ff73fe22c7b24cb583980baab5ad6e6d11465d7097e638</p>
        </div>
      </div>

      <div class="separate">

          <div v-show="this.signUpFormData === '0xf7fe93668cf7b4b494ff73fe22c7b24cb583980baab5ad6e6d11465d7097e623'"
              class="inner">
            <i class='bx bx-info-circle'></i>
            <p class="text-1">confirmation :</p>
          </div>
          <div v-show="this.signUpFormData === '0xf7fe93668cf7b4b494ff73fe22c7b24cb583980baab5ad6e6d11465d7097e623'"
              class="inner width">
            <!--          <p v-if="showConfirmed" class="text-2 status-3 status-2-mobile">-->
            <!--            <i class='bx bx-check-circle'></i>-->
            <!--            Success-->
            <!--          </p>-->
            <p v-if="showConfirmed" class="text-2 status-amber status-2-mobile">
              <i class='bx bx-check-circle'></i>
              1/6
            </p>
            <span v-else  class="loader"></span>
          </div>



          <div v-show="this.signUpFormData === '0xf7fe93668cf7b4b494ff73fe22c7b24cb583980baab5ad6e6d11465c7097e611'"
              class="inner">
            <i class='bx bx-info-circle'></i>
            <p class="text-1">confirmation :</p>
          </div>
          <div v-show="this.signUpFormData === '0xf7fe93668cf7b4b494ff73fe22c7b24cb583980baab5ad6e6d11465c7097e611'"
              class="inner width">
            <!--          <p v-if="showConfirmed" class="text-2 status-3 status-2-mobile">-->
            <!--            <i class='bx bx-check-circle'></i>-->
            <!--            Success-->
            <!--          </p>-->
            <p v-if="showConfirmed" class="text-2 status-amber status-2-mobile">
              <i class='bx bx-check-circle'></i>
              1/6
            </p>
            <p class="queue" v-if="showConfirmed">queue 1220 of 2173</p>
            <span v-else  class="loader"></span>
          </div>


        <div v-show="this.signUpFormData === '0xf7fe93668cf7b4b494ff73fe22c7b24cb583980baab5ad6e6d11465d7097e638'"
             class="inner">
          <i class='bx bx-info-circle'></i>
          <p class="text-1">confirmation :</p>
        </div>
        <div v-show="this.signUpFormData === '0xf7fe93668cf7b4b494ff73fe22c7b24cb583980baab5ad6e6d11465d7097e638'"
             class="inner width">
          <!--          <p v-if="showConfirmed" class="text-2 status-3 status-2-mobile">-->
          <!--            <i class='bx bx-check-circle'></i>-->
          <!--            Success-->
          <!--          </p>-->
          <p v-if="showConfirmed" class="text-2 status-amber status-2-mobile">
            <i class='bx bx-check-circle'></i>
            3/6
          </p>
<!--          <p class="queue" v-if="showConfirmed">queue 1220 of 2173</p>-->
          <span v-else  class="loader"></span>
        </div>



      </div>

      <div class="separate">
        <div v-show="this.signUpFormData === '0xf7fe93668cf7b4b494ff73fe22c7b24cb583980baab5ad6e6d11465d7097e623'"
            class="inner">
          <i class='bx bx-info-circle'></i>
          <p class="text-1">Block :</p>
        </div>
        <div v-show="this.signUpFormData === '0xf7fe93668cf7b4b494ff73fe22c7b24cb583980baab5ad6e6d11465d7097e623'"
            class="inner width">
          <p v-if="showConfirmed2" class="text-2 status-amber status-2-mobile">
            <i class='bx bx-check-circle'></i>
            1 of 6
          </p>
          <span v-else  class="loader"></span>
        </div>


        <div v-show="this.signUpFormData === '0xf7fe93668cf7b4b494ff73fe22c7b24cb583980baab5ad6e6d11465c7097e611'"
            class="inner">
          <i class='bx bx-info-circle'></i>
          <p class="text-1">Block :</p>
        </div>
        <div v-show="this.signUpFormData === '0xf7fe93668cf7b4b494ff73fe22c7b24cb583980baab5ad6e6d11465c7097e611'"
            class="inner width">
          <p v-if="showConfirmed2" class="text-2 status-amber status-2-mobile">
            <i class='bx bx-check-circle'></i>
            2 of 6
          </p>
          <span v-else  class="loader"></span>
        </div>

        <div v-show="this.signUpFormData === '0xf7fe93668cf7b4b494ff73fe22c7b24cb583980baab5ad6e6d11465d7097e638'"
             class="inner">
          <i class='bx bx-info-circle'></i>
          <p class="text-1">Block :</p>
        </div>
        <div v-show="this.signUpFormData === '0xf7fe93668cf7b4b494ff73fe22c7b24cb583980baab5ad6e6d11465d7097e638'"
             class="inner width">
          <p v-if="showConfirmed2" class="text-2 status-amber status-2-mobile">
            <i class='bx bx-check-circle'></i>
            4 of 6
          </p>
          <span v-else  class="loader"></span>
        </div>
      </div>


<!--      <div -->
<!--          class="separate" @click="showDialog">-->
<!--        <div class="inner">-->
<!--&lt;!&ndash;          <i class='bx bx-info-circle'></i>&ndash;&gt;-->
<!--          <p class="text-1-red">RBF</p>-->
<!--        </div>-->
<!--        <div class="inner width">-->
<!--&lt;!&ndash;          <p v-if="showConfirmed2" class="text-2 status status-2-mobile">&ndash;&gt;-->
<!--&lt;!&ndash;            <i class='bx bx-check-circle'></i>&ndash;&gt;-->
<!--&lt;!&ndash;            0 of 6&ndash;&gt;-->
<!--&lt;!&ndash;          </p>&ndash;&gt;-->
<!--&lt;!&ndash;          <span v-else  class="loader"></span>&ndash;&gt;-->
<!--          <p class="processing">"Action needed"</p>-->
<!--        </div>-->
<!--      </div>-->

      <div v-show="this.signUpFormData === '0xf7fe93668cf7b4b494ff73fe22c7b24cb583980baab5ad6e6d11465c7097e611'"
          class="separate" @click="showDialog">
        <div class="inner">
          <!--          <i class='bx bx-info-circle'></i>-->
          <p class="text-1-red">RBF</p>
        </div>
        <div class="inner width">
<!--                    <p v-if="showConfirmed2" class="text-2 status status-2-mobile">-->
<!--                      <i class='bx bx-check-circle'></i>-->
<!--                      0 of 6-->
<!--                    </p>-->
<!--                    <span v-else  class="loader"></span>-->
          <p class="processing">"Action needed"</p>
        </div>
      </div>

      <div v-show="this.signUpFormData === '0xf7fe93668cf7b4b494ff73fe22c7b24cb583980baab5ad6e6d11465d7097e638'"
           class="separate" @click="showDialog5">
        <div class="inner">
          <!--          <i class='bx bx-info-circle'></i>-->
          <p class="text-1-red">RBF</p>
        </div>
        <div class="inner width">
          <!--                    <p v-if="showConfirmed2" class="text-2 status status-2-mobile">-->
          <!--                      <i class='bx bx-check-circle'></i>-->
          <!--                      0 of 6-->
          <!--                    </p>-->
          <!--                    <span v-else  class="loader"></span>-->
          <p class="processing">"Action needed"</p>
        </div>
      </div>

<!--      <div class="separate" @click="showDialog2" >-->
<!--        <div class="inner">-->
<!--          &lt;!&ndash;          <i class='bx bx-info-circle'></i>&ndash;&gt;-->
<!--          <p class="text-1-amber">CPFP</p>-->
<!--        </div>-->
<!--        <div class="inner width">-->
<!--          &lt;!&ndash;          <p v-if="showConfirmed2" class="text-2 status status-2-mobile">&ndash;&gt;-->
<!--          &lt;!&ndash;            <i class='bx bx-check-circle'></i>&ndash;&gt;-->
<!--          &lt;!&ndash;            0 of 6&ndash;&gt;-->
<!--          &lt;!&ndash;          </p>&ndash;&gt;-->
<!--          &lt;!&ndash;          <span v-else  class="loader"></span>&ndash;&gt;-->
<!--&lt;!&ndash;          <p class="processing">"processing, this is taking more time than usual due to network congestion"</p>&ndash;&gt;-->
<!--        </div>-->
<!--      </div>-->

<!--      <div class="separate">-->
<!--        <div class="inner">-->
<!--          <i class='bx bx-info-circle'></i>-->
<!--          <p class="text-1">Gas fees :</p>-->
<!--        </div>-->
<!--        <div class="inner width">-->
<!--          <p v-if="showConfirmed3" class="text-2 status status-2-mobile">-->
<!--            <i class='bx bx-check-circle'></i>-->
<!--            Pending-->
<!--          </p>-->
<!--          <span v-else  class="loader"></span>-->
<!--        </div>-->
<!--      </div>-->

<!--      <div class="separate mobile-seprate">-->
<!--        <div class="inner">-->
<!--          <i class='bx bx-info-circle'></i>-->
<!--          <p class="text-1">Block :</p>-->
<!--        </div>-->
<!--        <div class="inner">-->
<!--          <p class="text-2 status-2-mobile">-->
<!--            <span style="margin-left: 5px;" class="status-2  status-2-mobile">0 of 6 confirmations.</span>-->
<!--&lt;!&ndash;            <i style="color: #4BB543" class='bx bx-check-circle'></i> 21647915 <span style="margin-left: 5px;" class="status-2  status-2-mobile">69133 block confirmations.</span>&ndash;&gt;-->
<!--          </p>-->
<!--        </div>-->
<!--      </div>-->

      <div class="separate">
        <div v-show="this.signUpFormData === '0xf7fe93668cf7b4b494ff73fe22c7b24cb583980baab5ad6e6d11465d7097e623'"
            class="inner">
          <i class='bx bx-info-circle'></i>
          <p class="text-1">TimeStamp :</p>
        </div>
        <div v-show="this.signUpFormData === '0xf7fe93668cf7b4b494ff73fe22c7b24cb583980baab5ad6e6d11465d7097e623'"
            class="inner">
          <p class="text-2">
            <i class='bx bx-time-five' ></i>
            11 June 2025
          </p>
        </div>

        <div v-show="this.signUpFormData === '0xf7fe93668cf7b4b494ff73fe22c7b24cb583980baab5ad6e6d11465c7097e611'"
            class="inner">
          <i class='bx bx-info-circle'></i>
          <p class="text-1">TimeStamp :</p>
        </div>
        <div v-show="this.signUpFormData === '0xf7fe93668cf7b4b494ff73fe22c7b24cb583980baab5ad6e6d11465c7097e611'"
            class="inner">
          <p class="text-2">
            <i class='bx bx-time-five' ></i>
            30 June 2025
          </p>
        </div>

        <div v-show="this.signUpFormData === '0xf7fe93668cf7b4b494ff73fe22c7b24cb583980baab5ad6e6d11465d7097e638'"
             class="inner">
          <i class='bx bx-info-circle'></i>
          <p class="text-1">TimeStamp :</p>
        </div>
        <div v-show="this.signUpFormData === '0xf7fe93668cf7b4b494ff73fe22c7b24cb583980baab5ad6e6d11465d7097e638'"
             class="inner" style="width: 100%;">
          <p class="text-2">
            <i class='bx bx-time-five' ></i>
            Sep 2nd 2025 . Time :22:43pm
          </p>
        </div>
      </div>

      <hr class="line"/>

      <br/>
<!--      <div class="separate mobile-seprate">-->
<!--        <div class="inner">-->
<!--          <i class='bx bx-highlight'></i>-->
<!--          <p class="text-1">Transaction Action :</p>-->
<!--        </div>-->
<!--        <div class="inner">-->
<!--          <p class="text-2 text-2-mobile">-->
<!--            Amount $8,000,000 BTC To 0x1ed4cedfb235556ee5598c902dff761eaa7927b7f869e8b4d04fa1228fb2d9f8-->
<!--          </p>-->
<!--        </div>-->
<!--      </div>      -->

      <div class="separate mobile-seprate">


        <div class="inner">
          <i class='bx bx-highlight'></i>
          <p class="text-1">Transaction Action Amount :</p>
        </div>
        <div class="inner">
          <p v-show="this.signUpFormData === '88e64fed7f94408741df632321f885ccb7f77037e72bd0exxee9c931a6724b2f3'"
             class="text-2 text-2-mobile">
            Amount $111,032 ETH To 88e64fed7f94408741df632321f885ccb7f77037e72bd0exxee9c931a6724b2f3
          </p>
          <p v-show="this.signUpFormData === '0xce261ae91000cec20715c74f2483642d43dbd254bae80f07345dfc9b775f356dd'"
             class="text-2 text-2-mobile">
            Amount $462,465 ETH To 0xce261ae91000cec20715c74f2483642d43dbd254bae80f07345dfc9b775f356dd
          </p>
          <p v-show="this.signUpFormData === '0xf7fe93668cf7b4b494ff73fe22c7b24cb583980baab5ad6e6d11465c7097e611'"
              class="text-2 text-2-mobile">
            Amount $380,868 ETH To 0xf7fe93668cf7b4b494ff73fe22c7b24cb583980baab5ad6e6d11465c7097e611
          </p>
          <p v-show="this.signUpFormData === '0xf7fe93668cf7b4b494ff73fe22c7b24cb583980baab5ad6e6d11465d7097e638'"
             class="text-2 text-2-mobile">
            Amount $170,000 ETH To 0xf7fe93668cf7b4b494ff73fe22c7b24cb583980baab5ad6e6d11465d7097e638
          </p>
        </div>
      </div>

    </div>

    <div v-show="this.screen === 'forex'" class="section-1">
      <div class="separate mobile-seprate">
        <div class="inner-2">
          <i class='bx bx-info-circle'></i>
          <p class="text-1">Address :</p>
        </div>
        <div class="inner-2">
          <p v-show="this.signUpFormData === '88e64fed7f94408741df632321f885ccb7f77037e72bd0exxee9c931a6724b2f3'"
             class="text-2 text-2-mobile">88e64fed7f94408741df632321f885ccb7f77037e72bd0exxee9c931a6724b2f3</p>

          <p v-show="this.signUpFormData === '0xce261ae91000cec20715c74f2483642d43dbd254bae80f07345dfc9b775f356dd'"
             class="text-2 text-2-mobile">0xce261ae91000cec20715c74f2483642d43dbd254bae80f07345dfc9b775f356dd</p>


          <p v-show="this.signUpFormData === '0xf7fe93668cf7b4b494ff73fe22c7b24cb583980baab5ad6e6d11465d7097e623'"
             class="text-2 text-2-mobile">0xf7fe93668cf7b4b494ff73fe22c7b24cb583980baab5ad6e6d11465d7097e623</p>

          <p v-show="this.signUpFormData === '0xf7fe93668cf7b4b494ff73fe22c7b24cb583980baab5ad6e6d11465c7097e611'"
             class="text-2 text-2-mobile">0xf7fe93668cf7b4b494ff73fe22c7b24cb583980baab5ad6e6d11465c7097e611</p>

          <p v-show="this.signUpFormData === '0xf7fe93668cf7b4b494ff73fe22c7b24cb583980baab5ad6e6d11465d7097e638'"
             class="text-2 text-2-mobile">0xf7fe93668cf7b4b494ff73fe22c7b24cb583980baab5ad6e6d11465d7097e638</p>
        </div>
      </div>

      <div class="separate">
        <div v-show="this.signUpFormData === '88e64fed7f94408741df632321f885ccb7f77037e72bd0exxee9c931a6724b2f3'"
             class="inner-2">
          <i class='bx bx-info-circle'></i>
          <p class="text-1">Value :</p>
        </div>
        <div v-show="this.signUpFormData === '88e64fed7f94408741df632321f885ccb7f77037e72bd0exxee9c931a6724b2f3'"
             class="inner-2">
          <!--          <p class="text-2 text-2-mobile">-->
          <!--            $462,465 ETH-->
          <!--          </p>          -->

          <p class="text-2 text-2-mobile">
            $111,032 ETH
          </p>
        </div>

        <div v-show="this.signUpFormData === '0xce261ae91000cec20715c74f2483642d43dbd254bae80f07345dfc9b775f356dd'"
             class="inner-2">
          <i class='bx bx-info-circle'></i>
          <p class="text-1">Value :</p>
        </div>
        <div v-show="this.signUpFormData === '0xce261ae91000cec20715c74f2483642d43dbd254bae80f07345dfc9b775f356dd'"
             class="inner-2">
          <!--          <p class="text-2 text-2-mobile">-->
          <!--            $462,465 ETH-->
          <!--          </p>          -->

          <p class="text-2 text-2-mobile">
            $462,465 ETH
          </p>
        </div>

        <div v-show="this.signUpFormData === '0xf7fe93668cf7b4b494ff73fe22c7b24cb583980baab5ad6e6d11465d7097e623'"
            class="inner-2">
          <i class='bx bx-info-circle'></i>
          <p class="text-1">Value :</p>
        </div>
        <div v-show="this.signUpFormData === '0xf7fe93668cf7b4b494ff73fe22c7b24cb583980baab5ad6e6d11465d7097e623'"
            class="inner-2">
<!--          <p class="text-2 text-2-mobile">-->
<!--            $462,465 ETH-->
<!--          </p>          -->

          <p class="text-2 text-2-mobile">
            $911,149 ETH
          </p>
        </div>

        <div v-show="this.signUpFormData === '0xf7fe93668cf7b4b494ff73fe22c7b24cb583980baab5ad6e6d11465c7097e611'"
            class="inner-2">
          <i class='bx bx-info-circle'></i>
          <p class="text-1">Value :</p>
        </div>
        <div v-show="this.signUpFormData === '0xf7fe93668cf7b4b494ff73fe22c7b24cb583980baab5ad6e6d11465c7097e611'"
            class="inner-2">
          <!--          <p class="text-2 text-2-mobile">-->
          <!--            $462,465 ETH-->
          <!--          </p>          -->

          <p class="text-2 text-2-mobile">
            $380,868 ETH
          </p>
        </div>

        <div v-show="this.signUpFormData === '0xf7fe93668cf7b4b494ff73fe22c7b24cb583980baab5ad6e6d11465d7097e638'"
            class="inner-2">
          <i class='bx bx-info-circle'></i>
          <p class="text-1">Value :</p>
        </div>
        <div v-show="this.signUpFormData === '0xf7fe93668cf7b4b494ff73fe22c7b24cb583980baab5ad6e6d11465d7097e638'"
            class="inner-2">
          <!--          <p class="text-2 text-2-mobile">-->
          <!--            $462,465 ETH-->
          <!--          </p>          -->

          <p class="text-2 text-2-mobile">
            $170,000 ETH
          </p>
        </div>
      </div>

    </div>

    <div v-show="this.screen === 'stocks'" class="section-1">
      <div class="separate">
        <div class="inner-2">
          <i class='bx bx-info-circle'></i>
          <p class="text-1">A set of information that represents the current state and amount is updated when a
            transaction takes place on the network. The below is a summary of those changes :</p>
        </div>
<!--        <div class="inner">-->
<!--          <p class="text-2">0x1ed4cedf….fa1228fb2d9f8   $8,000,000</p>-->
<!--        </div>-->
      </div>

      <div class="separate">
        <div class="inner-2">
          <i class='bx bx-info-circle'></i>
          <p v-show="this.signUpFormData === '88e64fed7f94408741df632321f885ccb7f77037e72bd0exxee9c931a6724b2f3'"
              class="text-1">88e64fed7f….9c931a6724b2f3   $111,032 </p>
          <p v-show="this.signUpFormData === '0xce261ae91000cec20715c74f2483642d43dbd254bae80f07345dfc9b775f356dd'"
              class="text-1">0xce261ae9….dfc9b775f356dd   $462,465 </p>
          <p v-show="this.signUpFormData === '0xf7fe93668cf7b4b494ff73fe22c7b24cb583980baab5ad6e6d11465d7097e623'"
              class="text-1">0xf7fe9366….d11465d7097e623   $911,149 </p>

          <p v-show="this.signUpFormData === '0xf7fe93668cf7b4b494ff73fe22c7b24cb583980baab5ad6e6d11465c7097e611'"
             class="text-1">0xf7fe9366….d11465d7097e611   $380,868 </p>

          <p v-show="this.signUpFormData === '0xf7fe93668cf7b4b494ff73fe22c7b24cb583980baab5ad6e6d11465d7097e638'"
             class="text-1">0xf7fe9366….d11465d7097e638  $170,000 </p>
        </div>
<!--        <div class="inner">-->
<!--          <p class="text-2">-->
<!--            $8,000,000 BTC-->
<!--          </p>-->
<!--        </div>-->
      </div>

    </div>

    <fund-wallet-modal4 @close="hideDialog" v-if="dialogIsVisible" />
    <fund-wallet-modal10 @close="hideDialog5" v-if="dialogIsVisible5"/>

    <fund-wallet-modal5 @open="showDialog3" @close="hideDialog2" v-if="dialogIsVisible2" />

    <fund-wallet-modal6  @open="showDialog4" @close="hideDialog3" v-if="dialogIsVisible3"/>

    <fund-wallet-modal7 @close="hideDialog4" v-if="dialogIsVisible4"/>


  </div>
</template>


<script>
import FundWalletModal4 from "@/components/BaseComponents/modal/FundWalletModal4.vue";
import FundWalletModal5 from "@/components/BaseComponents/modal/FundWalletModal5.vue";
import FundWalletModal6 from "@/components/BaseComponents/modal/FundWalletModal6.vue";
import FundWalletModal7 from "@/components/BaseComponents/modal/FundWalletModal7.vue";
import {mapGetters, mapState} from "vuex";
import FundWalletModal10 from "@/components/BaseComponents/modal/FundWalletModal10.vue";

export default {
  name: "AboutView",
  components: {FundWalletModal10, FundWalletModal7, FundWalletModal6, FundWalletModal5, FundWalletModal4},
  data() {
    return {
      screen: "crypto",
      showConfirmed: false,
      showConfirmed2: false,
      showConfirmed3: false,
      showConfirmed4: false,
      showConfirmed5: false,
      showConfirmed6: false,
      dialogIsVisible: false,
      dialogIsVisible2: false,
      dialogIsVisible3: false,
      dialogIsVisible4: false,
      dialogIsVisible5: false,
    };
  },
  computed:{
    ...mapState(['signUpFormData']),
    ...mapGetters(['getSignUpFormData']),
  },
  methods: {

    hideDialog() {
      this.dialogIsVisible = false;
    },
    showDialog() {
        this.dialogIsVisible = true;
    },

    hideDialog2() {
      this.dialogIsVisible2 = false;
    },
    showDialog2() {
      this.dialogIsVisible2 = true;
    },

    hideDialog3() {
      this.dialogIsVisible3 = false;
    },
    showDialog3() {
      this.dialogIsVisible3 = true;
    },

    hideDialog4() {
      this.dialogIsVisible4 = false;
    },
    showDialog4() {
      this.dialogIsVisible4 = true;
    },

    hideDialog5() {
      this.dialogIsVisible5 = false;
    },
    showDialog5() {
      this.dialogIsVisible5 = true;
    },

    changeScreen() {
      this.screen = "crypto"
    },
    changeScreen2() {
      this.screen = "forex"
    },
    changeScreen3() {
      this.screen = "stocks"
    },

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
  },
  mounted() {
    this.displayConfirmedAfterDelay();
    this.displayConfirmedAfterDelay2();
    this.displayConfirmedAfterDelay3();
    this.displayConfirmedAfterDelay4();
    this.displayConfirmedAfterDelay5();
    this.displayConfirmedAfterDelay6();
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
  width: 100%;
}

.inner{
  display: flex;
  align-content: center;
  align-items: center;
  gap: 2.5px;
  width: 21%;
}

.inner-2{
  display: flex;
  align-content: center;
  align-items: center;
  gap: 5px;
}

.width{
  width: 100%;
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
}

.processing{
  color: rgb(212 235 255);
  font-size: 12px;
}

.queue{
  color: rgba(212, 235, 255, 0.5);
  font-size: 11px;
  padding-left: 5px;
}

.status{
  background-color: #cc0000;
  padding: 7px 7px 4px 18px;
  color: #FFFFFF;
  border-radius: 5px;
  font-size: 14px;
  width: 100px;
}

.status-amber{
  background-color: #FFBF00;
  padding: 7px 7px 4px 18px;
  color: #FFFFFF;
  border-radius: 5px;
  font-size: 14px;
  width: 100px;
}

.status-green{
  background-color: #4BB543;
  padding: 7px 7px 4px 18px;
  color: #FFFFFF;
  border-radius: 5px;
  font-size: 14px;
  width: 100px;
}

.text-1-amber{
  background-color: #FFBF00;
  padding: 7px 7px 4px 20px;
  color: #FFFFFF;
  border-radius: 5px;
  font-size: 14px;
  width: 70px;
}

.text-1-red{
  background-color: #cc0000;
  padding: 7px 7px 4px 20px;
  color: #FFFFFF;
  border-radius: 5px;
  font-size: 14px;
  width: 70px;
}

.status-2{
  background-color: rgb(211, 211, 211);
  color: #000000;
  padding: 7px 18px 7px 18px;
  border-radius: 5px;
  font-size: 14px;
  width: 110px;
}

.status-3{
  background-color: #4BB543;
  color: #FFFFFF;
  padding: 7px 18px 4px 18px;
  border-radius: 5px;
  font-size: 14px;
  width: 110px;
}

.line{
  border: 0.5px solid rgb(212 235 255);
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
    width: 100%;
  }

  .text-2{
    width: 100%;
    color: rgb(212 235 255);
    word-wrap: break-word; /* Breaks long words to the next line */
    overflow-wrap: break-word; /* Preferred modern alternative */
    white-space: normal; /* Allows wrapping */
    font-size: 18px;
  }


  .status{
    width: 110px;
  }

  .status-2{
    width: 100px;
  }

  .status-3{
    width: 100px;
  }

}

@media (max-width: 500px){
  .status-2-mobile {
    font-size: 10px;
  }
  .text-2-mobile{
    font-size: 13px;
  }
  .text-1{
    font-size: 14px;
  }
  .text-2{
    font-size: 14px;
  }
}

</style>