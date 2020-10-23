<template>
<link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/font-awesome/4.7.0/css/font-awesome.min.css" integrity="sha384-wvfXpqpZZVQGK6TAh5PVlGOfQNHSoD2xbE+QkPxCAFlNEevoEH3Sl0sibVcOQVnN" crossorigin="anonymous">
  <base-container>
    <center>You have {{money}} $ now</center>
    <br>
    <center>
      Apple: {{appleCount}}, Grape: {{grapeCount}}
       <!-- Water: {{WaterCount}}, Suger: {{SugerCount}} -->
      <br>
      Apple Juice: {{appleJuiceCount}}, Grape Juice: {{grapeJuiceCount}}
      <br>
      <br>
      <button @click="giveMoney" class="moneyButton"> Give me money (0.25$ - 2.0$)</button>&nbsp;
      <br><br>
      <button @click="freeMoney(1000000)" class="moneyButton"> Free 1000000$ (This will break the balance for sho tho)</button>
      
    </center>
  </base-container>


  <base-container title="Market" >
  <i class="fas fa-store"></i>
    <button @click="toggleDisplayMarket" v-if="!MarketOpen" class="toogleButton"> +</button>
    <button @click="toggleDisplayMarket" v-else class="toogleButton">-</button>
    <div v-if="MarketOpen">
      <form @submit.prevent="buyItem">
        <div class="form-control">
          <h2>What do you want to buy? </h2> 
          <div>
            <input name="market-apple" type="radio" value="apple" v-model="market" />
            <label for="market-apple">Apple(0.5 $)</label>
          </div>
          <div>
            <input name="market-grape" type="radio" value="grape" v-model="market" />
            <label for="market-grape">Grape(0.75 $)</label>
          </div>
        </div>
        <div>
            
            <button @click="buyItem(1)">Buy 1</button>&nbsp;
            <button @click="buyItem(2)">2</button>&nbsp;
            <button @click="buyItem(5)">5</button>&nbsp;
            <br>
            <button @click="buyItem(10)">10</button>&nbsp;
            <button @click="buyItem(25)">25</button>&nbsp;
            <button @click="buyItem(50)">50</button>&nbsp;
            <button @click="buyItem(100)">100</button>&nbsp;
            <br>
            <button @click="buyItem(200)">200</button>&nbsp;
            <button @click="buyItem(300)">300</button>&nbsp;
            <button @click="buyItem(400)">400</button>&nbsp;
            <button @click="buyItem(500)">500</button>&nbsp;
            <button @click="buyItem(1000)">1000</button>&nbsp;
        </div>
      </form>
      <button @click="buyMax">Buy Max</button><br><br>
    </div>

  </base-container>

  <base-container :title="'Factory Lv.' + machineCount" >
    <button @click="toggleDisplayFactory" v-if="!FactoryOpen" class="toogleButton"> +</button>
    <button @click="toggleDisplayFactory" v-else class="toogleButton"> -</button>
    <div v-if="FactoryOpen">
      <form @submit.prevent="makeDrink">
        <div class="form-control">
          <h2>What do you want to mix it?</h2>
          <div>
            <input name="mix-apple" type="radio" value="appleJuice" v-model="mix" />
            <label for="mix-apple">Apple Juice</label>
          </div>
          <div>
            <input name="mix-grape" type="radio" value="grapeJuice" v-model="mix" />
            <label for="mix-grape">Grape juice</label>
          </div>
        </div>
        <button @click="makeMaxDrink">Make max count out of it</button>
        <br><br>
        <div>
          <div v-if="machineCount === 1">
            <button @click="makeDrink(1,4)">Make 1 from 4</button>&nbsp;
            <button @click="makeDrink(2,4)">2</button>&nbsp;
            <button @click="makeDrink(5,4)">5</button>&nbsp;
            <br>
            <button @click="makeDrink(10,4)">10</button>&nbsp;
            <button @click="makeDrink(25,4)">25</button>&nbsp;
            <button @click="makeDrink(50,4)">50</button>&nbsp;
            <button @click="makeDrink(100,4)">100</button>&nbsp;
            
            <br><br>
            <button @click="buyMachine(500)" class="buyList">Unlock the better machine(1 from 3!  500$)</button>
          </div>
          <div v-if="machineCount === 2">
            <button @click="makeDrink(1,3)">Make 1 from 3</button>&nbsp;
            <button @click="makeDrink(2,3)">2</button>&nbsp;
            <button @click="makeDrink(5,3)">5</button>&nbsp;
            <br>
            <button @click="makeDrink(10,3)">10</button>&nbsp;
            <button @click="makeDrink(25,3)">25</button>&nbsp;
            <button @click="makeDrink(50,3)">50</button>&nbsp;
            <button @click="makeDrink(100,3)">100</button>&nbsp;

            <br><br>
            <button  @click="buyMachine(2000)" class="buyList">Unlock the better machine(1 from 2!  2000$)</button>
          </div>
          <div v-if="machineCount === 3">
            <button @click="makeDrink(1,2)">Make 1 from 2</button>&nbsp;
            <button @click="makeDrink(2,2)">2</button>&nbsp;
            <button @click="makeDrink(5,2)">5</button>&nbsp;
            <br>
            <button @click="makeDrink(10,2)">10</button>&nbsp;
            <button @click="makeDrink(25,2)">25</button>&nbsp;
            <button @click="makeDrink(50,2)">50</button>&nbsp;
            <button @click="makeDrink(100,2)">100</button>&nbsp;

            <br><br>
            <button  @click="buyMachine(50000)" class="buyList">Unlock the better machine(1 from 1!  50000$)</button>
          </div>
          <div v-if="machineCount === 4">
            <button @click="makeDrink(1,1)">Make 1 from 1</button>&nbsp;
            <button @click="makeDrink(2,1)">2</button>&nbsp;
            <button @click="makeDrink(5,1)">5</button>&nbsp;
            <br>
            <button @click="makeDrink(10,1)">10</button>&nbsp;
            <button @click="makeDrink(25,1)">25</button>&nbsp;
            <button @click="makeDrink(50,1)">50</button>&nbsp;
            <button @click="makeDrink(100,1)">100</button>&nbsp;

            <br><br>
            <button  @click="buyMachine(100000)" class="buyList">Unlock the better machine(2 from 1!  100000$)</button>
          </div>
          <div v-if="machineCount === 5">
            <button @click="makeDrink(1,0.5)">Make 1 from 0.5</button>&nbsp;
            <button @click="makeDrink(2,0.5)">2</button>&nbsp;
            <button @click="makeDrink(5,0.5)">5</button>&nbsp;
            <br>
            <button @click="makeDrink(10,0.5)">10</button>&nbsp;
            <button @click="makeDrink(25,0.5)">25</button>&nbsp;
            <button @click="makeDrink(50,0.5)">50</button>&nbsp;
            <button @click="makeDrink(100,0.5)">100</button>&nbsp;

            <br><br>
            <button v-if="machineCount === 5"> you rich dude</button>
            <!-- <button  @click="buyMachine(100000)" class="buyList">Unlock the better machine(2 from 1!  100000$)</button> -->
          </div>
          
        </div>
      </form>
    </div>
  </base-container>

  <!-- I hide this section -->
  <base-container title="Storage" v-if="StorageOpen" >
  <button @click="toggleDisplayStorage" v-if="!StorageOpen" class="toogleButton"> +</button>
  <button @click="toggleDisplayStorage" v-else class="toogleButton"> -</button>
  </base-container>

  <base-container title="Store">
    <button @click="toggleDisplayStore" v-if="!StoreOpen" class="toogleButton"> +</button>
    <button @click="toggleDisplayStore" v-else class="toogleButton"> -</button>
    <div v-if="StoreOpen">
      <form @submit.prevent="sellMultiple">
        <div class="form-control">
          <h2>What do you want to sel it</h2>
          <div>
            <input name="mix-apple" type="radio" value="appleJuice" v-model="sell" />
            <label for="mix-apple">Apple Juice(3 $)</label>
          </div>
          <div> 
            <input name="mix-grape" type="radio" value="grapeJuice" v-model="sell" />
            <label for="mix-grape">Grape Juice(5 $)</label>
          </div>
        </div>
        <div>
          <button @click="sellMultiple(1)">Sell the item</button>
          <button @click="sellMultiple(10)">Sell (x10)</button>
          <button @click="sellMultiple(25)">Sell (x25)</button>
          <button @click="sellMultiple(50)">Sell (x50)</button>
          <button @click="sellMultiple(100)">Sell (x100)</button>

        </div>
      </form>
        <button @click="sellAll(1)">Sell all Apple Juice</button>&nbsp;
        <button @click="sellAll(2)">Sell all Grape Juice</button>&nbsp;
        <button @click="sellAll(0)">Sell all Everything</button>
    </div>
  </base-container>

  <base-container title="Online Order">
    <button @click="toggleDisplayOnlineOrder" v-if="!OnlineOrderOpen" class="toogleButton"> +</button>
    <button @click="toggleDisplayOnlineOrder" v-else class="toogleButton"> -</button>
    <div v-if="OnlineOrderOpen">
      <br>
      <center><button v-if="checkCount === 0" @click="catering" class="chekDealButton">Unlock the catering order with better deal! (2000$)</button></center>
      <div v-if="checkCount !== 0">
        <form @submit.prevent="completeOnlinOrder">
          <div class="form-control" >
            <h2>Which online order should we do?</h2>
            <h3>The price is {{randomOdds * 100}}% higher this time!</h3>
            <h4>400% is the highest deal</h4>
            <div>
              <input name="online-1" type="radio" value="1" v-model="online" />
              <label for="online-1">
                AppleJuice: {{apple1}}. GrapeJuice: {{grape1}}. in total: 10 <br>
                &nbsp; &nbsp; &nbsp; &nbsp;  The original price: {{og1}}$, after deal: {{odds1}}$
                <br>&nbsp; &nbsp; &nbsp; &nbsp; The cost: {{cost1}}$, the pure profit is: {{pureProfit1}}$
              </label>
            </div>
            <br>
            <div>
              <input name="online-2" type="radio" value="2" v-model="online" />
              <label for="online-2">
                AppleJuice: {{apple2}}. GrapeJuice: {{grape2}}. in total: 50<br>
                &nbsp; &nbsp; &nbsp; &nbsp;  The original price: {{og2}}$, after deal: {{odds2}}$
                <br>&nbsp; &nbsp; &nbsp; &nbsp; The cost: {{cost2}}$, the pure profit is: {{pureProfit2}}$
                
              </label>
            </div>
            <br>
            <div>
              <input name="online-3" type="radio" value="3" v-model="online" />
              <label for="online-3">
                AppleJuice: {{apple3}}. GrapeJuice: {{grape3}}. in total: 100<br>
                &nbsp; &nbsp; &nbsp; &nbsp;  The original price: {{og3}}$, after deal: {{odds3}}$
                <br>&nbsp; &nbsp; &nbsp; &nbsp; The cost: {{cost3}}$, the pure profit is: {{pureProfit3}}$
              </label>
            </div>
            <br>
            <div>
              <input name="online-4" type="radio" value="4" v-model="online" />
              <label for="online-4">
                AppleJuice: {{apple4}}. GrapeJuice: {{grape4}}. in total: 250 <br>
                &nbsp; &nbsp; &nbsp; &nbsp;  The original price: {{og4}}$, after deal: {{odds4}}$
                <br>&nbsp; &nbsp; &nbsp; &nbsp; The cost: {{cost4}}$, the pure profit is: {{pureProfit4}}$
              </label>
            </div>
            <br>
            <div>
              <input name="online-5" type="radio" value="5" v-model="online" />
              <label for="online-5">
                AppleJuice: {{apple5}}. GrapeJuice: {{grape5}}. in total: 500 <br>
                &nbsp; &nbsp; &nbsp; &nbsp;  The original price: {{og5}}$, after deal: {{odds5}}$
                <br>&nbsp; &nbsp; &nbsp; &nbsp; The cost: {{cost5}}$, the pure profit is: {{pureProfit5}}$
              </label>
            </div>
            <br>
            <div>
              <input name="online-6" type="radio" value="6" v-model="online" />
              <label for="online-6">
                AppleJuice: {{apple6}}. GrapeJuice: {{grape6}}. in total: 1000 <br>
                &nbsp; &nbsp; &nbsp; &nbsp;  The original price: {{og6}}$, after deal: {{odds6}}$
                <br>&nbsp; &nbsp; &nbsp; &nbsp; The cost: {{cost6}}$, the pure profit is: {{pureProfit6}}$
              </label>
            </div>
            <br>
          </div>
          <div>
            <button>Complete the online order</button>
            <br><br>
            <button @click="refresh" class="refreshButton">Pay 5$ to refresh the deal!</button>

          </div>
        </form>
      </div>
    </div>
  </base-container>

  <base-container>
    <center>You have {{money}} $ now</center>
    <br>
    <center>
      Apple: {{appleCount}}, Grape: {{grapeCount}}
       <!-- Water: {{WaterCount}}, Suger: {{SugerCount}} -->
      <br>
      Apple Juice: {{appleJuiceCount}}, Grape Juice: {{grapeJuiceCount}}
      <br>
      <br>
      <button @click="giveMoney" class="moneyButton"> Give me money (0.25$ - 2.0$)</button>&nbsp;
      <br><br>
      <button @click="freeMoney(1000000)" class="moneyButton"> Free 1000000$ (This will break the balance for sho tho)</button>
      
    </center>
  </base-container>

  <base-container title="Cheating Box">
    <button @click="toggleDisplayCheatin" v-if="!Cheatingopen" class="toogleButton"> +</button>
    <button @click="toggleDisplayCheatin" v-else class="toogleButton"> -</button>
    <div v-if="Cheatingopen">
      <form @submit.prevent="sellMultiple">
        <div class="form-control">
          <h2>Wassup cheater</h2>
          <div>
            <input name="cheat-apple" type="radio" value="appleJuice" v-model="cheat" />
            <label for="cheat-apple">Apple Juice</label>
          </div>
          <div> 
            <input name="cheat-grape" type="radio" value="grapeJuice" v-model="cheat" />
            <label for="cheat-grape">Grape Juice</label>
          </div>
          <div> 
            <input name="cheat-money" type="radio" value="money" v-model="cheat" />
            <label for="cheat-money">Money</label>
          </div>
        </div>
        <div>
          <button @click="cheatingGame(1)">1</button>&nbsp;
          <button @click="cheatingGame(5)">5</button>&nbsp;
          <button @click="cheatingGame(10)">10</button>&nbsp;
          <button @click="cheatingGame(25)">25</button>&nbsp;
          <button @click="cheatingGame(50)">50</button>&nbsp;
          <br><br>
          <button @click="cheatingGame(100)">100</button>&nbsp;
          <button @click="cheatingGame(200)">200</button>&nbsp;
          <button @click="cheatingGame(500)">500</button>&nbsp;
          <button @click="cheatingGame(1000)">1000</button>&nbsp;
          <button @click="cheatingGame(10000)">10000</button>&nbsp;

        </div>
      </form>
    </div>
  </base-container>

</template>


<script>
import BaseContainer from './components/BaseContainer.vue';

var spendAudio = new Audio('/audio/spend.wav')
var getPaidAudio = new Audio('/audio/getPaid.wav')
var getPaidALotAudio = new Audio('/audio/getPaidAlot.wav')
var nopeAudio = new Audio('/audio/nope.m4a')
var pouringAudio = new Audio('/audio/pouring.mp3')
var letmeseeAudio = new Audio('/audio/hmm.wav')
var machineAudio = new Audio('/audio/machine.wav')
var sighAudio = new Audio('/audio/sigh.wav')
var onlineOrderAudio = new Audio('/audio/onlineOrder.wav')
var honkAudio = new Audio('/audio/honkAudio.wav')
var cheatingAudio = new Audio('/audio/cheating.wav')

export default{
  data(){
    return{
      MarketOpen: false,
      FactoryOpen: false,
      StorageOpen: false,
      StoreOpen: false,
      OnlineOrderOpen: false,
      Cheatingopen: false,
      money: 100,
      appleCount: 5,
      appleJuiceCount: 3,
      grapeCount: 5,
      grapeJuiceCount: 3,
      WaterCount: 2,
      SugerCount: 2,
      mix: null,
      sell: null,
      market: null,
      num : null,
      marketPrice: null,

      machineCount: 1,
      checking: false,

      randomNum: null,
      randomOdds: null,
      online: null,
      checkCount: 0,
  
      apple1: null,
      grape1: null,
      og1: null,
      odds1: null,
      pureProfit1: null,
      cost1: null,
      apple2: null,
      grape2: null,
      og2: null,
      odds2: null,
      pureProfit2: null,
      cost2: null,
      apple3: null,
      grape3: null,
      og3: null,
      odds3: null,
      pureProfit3: null,
      cost3: null,
      
      apple4: null,
      grape4: null,
      og4: null,
      odds4: null,
      pureProfit4: null,
      cost4: null,

      apple5: null,
      grape5: null,
      og5: null,
      odds5: null,
      pureProfit5: null,
      cost5: null,
      
      apple6: null,
      grape6: null,
      og6: null,
      odds6: null,
      pureProfit6: null,
      cost6: null,


      levelCal: null,

      cheat: null,

      MaxApple: null,
      MaxGrape: null,
      MaxConfirm: false,

      MaxMarket: null,
      confirmMarket: false,

      countRandom: 0,

      sellConfirm: false,
      sellAllPrice: 0,

      cateringCheck: false,
    }
  },
  components: {
    BaseContainer,
  },
  methods: {
    isMarketOpen() {
      return this.$store.getters.userIsAuthenticated;
    },
    toggleDisplayMarket(){
      this.MarketOpen = !this.MarketOpen
    },
    toggleDisplayFactory(){
      this.FactoryOpen = !this.FactoryOpen
    },
    toggleDisplayStorage(){
      this.StorageOpen = !this.StorageOpen
    },
    toggleDisplayStore(){
      this.StoreOpen = !this.StoreOpen
    },  
    toggleDisplayOnlineOrder(){
      this.OnlineOrderOpen = !this.OnlineOrderOpen
    }, 
    toggleDisplayCheatin(){
      this.Cheatingopen = !this.Cheatingopen
    }, 
    buyMax(){
      if(this.market !== null){
        if(this.market === 'apple'){
          if(this.money >= 0.5){
            this.marketPrice = 0.5
            this.MaxMarket = Math.floor(this.money / this.marketPrice)
            this.confirmMarket = confirm(`Would you like to buy ${this.MaxMarket} ${this.market}  with ${this.MaxMarket * this.marketPrice}$ ?`)
            if(this.confirmMarket){
              this.appleCount = this.appleCount + this.MaxMarket
              this.money = this.money - (this.MaxMarket * this.marketPrice)
              spendAudio.play()
              setTimeout(this.delayedMarket, 750)
              setTimeout(this.delayedMarket, 1500)

            }else{
              sighAudio.play();
            }
          }else{
            nopeAudio.play()
            alert("get your broke ass out this market")
          }
        }else if(this.market === 'grape'){
          if(this.money >= 0.75){
            this.marketPrice = 0.75
            this.MaxMarket = Math.floor(this.money / this.marketPrice)
            this.confirmMarket = confirm(`Would you like to buy ${this.MaxMarket} ${this.market}  with ${this.MaxMarket * this.marketPrice}$ ?`)
            if(this.confirmMarket){
              this.grapeCount = this.grapeCount + this.MaxMarket
              this.money = this.money - (this.MaxMarket * this.marketPrice)
              spendAudio.play()
              setTimeout(this.delayedMarket, 750)
              setTimeout(this.delayedMarket, 1500)
            }else{
              sighAudio.play();
            }
          }else{
            nopeAudio.play()
            alert("get your broke ass out this market")
          }
        }
      }
    },  
    buyItem(num){
      if(num){
        if(this.market !== null){
        if(this.market === 'apple'){
          this.marketPrice = 0.5
        }else if(this.market === 'grape'){
          this.marketPrice = 0.75
        }else if(this.market === 'water'){
          this.marketPrice = 1
        }else if(this.market === 'suger'){
          this.marketPrice = 0.5
        }
        


        if(this.money - (this.marketPrice * num) >= 0){
          this.money = this.money - (this.marketPrice * num);
          if(this.market === 'apple'){
            this.appleCount = this.appleCount + num;
          }else if(this.market === 'grape'){
            this.grapeCount = this.grapeCount + num;
          }else if(this.market === 'water'){
            this.WaterCount = this.grapeCount + num
          }else if(this.market === 'suger'){
            this.SugerCount = this.SugerCount + num
          }
          spendAudio.play();
          console.log('thanks for buying it')
        }else{
          nopeAudio.play()
          alert("get your broke ass out this market")
        }
        this.market = null;
      }
      }
      
    },
    sellAll(item){
      if(item === 0){
        if(!(this.appleJuiceCount === 0 && this.grapeJuiceCount === 0)){
          this.sellAllPrice = (this.appleJuiceCount * 3) + (this.grapeJuiceCount * 5)
          this.sellConfirm = confirm(`Would you like to sell all of your apple juice and grape juice for ${this.sellAllPrice}$ ? `)
          if(this.sellConfirm){
            this.appleJuiceCount = 0;
            this.grapeJuiceCount = 0;
            this.money = this.money + this.sellAllPrice;
            getPaidAudio.play()
            setTimeout(this.delayedPaid, 750)
            setTimeout(this.delayedPaid, 1500)
          }else{
            sighAudio.play()
          }
        }else{
          nopeAudio.play()
          alert("You don't have anything")
        }
        
      }else if(item === 1){
        if(this.appleJuiceCount > 0){
          this.sellAllPrice = (this.appleJuiceCount * 3) 
          this.sellConfirm = confirm(`Would you like to sell all of your apple juice for ${this.sellAllPrice}$ ? `)
          if(this.sellConfirm){
            this.appleJuiceCount = 0;
            this.money = this.money + this.sellAllPrice;
            getPaidAudio.play()
            setTimeout(this.delayedPaid, 750)
            setTimeout(this.delayedPaid, 1500)
          }else{
            sighAudio.play()
          }
        }else{
          nopeAudio.play()
          alert("You don't have any apple juice!")
        }

      }else if(item === 2){
        if(this.grapeJuiceCount > 0){
          this.sellAllPrice = (this.grapeJuiceCount * 5)
          this.sellConfirm = confirm(`Would you like to sell all of your grape juice for ${this.sellAllPrice}$ ? `)
          if(this.sellConfirm){
            this.grapeJuiceCount = 0;
            this.money = this.money + this.sellAllPrice;
            getPaidAudio.play()
            setTimeout(this.delayedPaid, 750)
            setTimeout(this.delayedPaid, 1500)
          }else{
            sighAudio.play()
          }
        }else{
          nopeAudio.play()
          alert("You don't have any apple juice!")
        }
      }

    },
    sellMultiple(multipleNum){
      if(this.sell === 'appleJuice'){
          if(this.appleJuiceCount< multipleNum){
            nopeAudio.play()
            alert(`You don't have ${multipleNum} of the selected item`)
          }else{
            this.appleJuiceCount = this.appleJuiceCount - multipleNum
            this.money = this.money + (3 * multipleNum)
            getPaidALotAudio.play();
          }
        }else if(this.sell === 'grapeJuice'){
          if(this.grapeJuiceCount< multipleNum){
            nopeAudio.play()
            alert(`You don't ${multipleNum} of the selected item`)
          }else{
            this.grapeJuiceCount = this.grapeJuiceCount - multipleNum
            this.money = this.money + (5 * multipleNum)
            getPaidAudio.play();
          }
        }
        this.sell = null;
    },
    cheatingGame(count){
      if(this.cheat === 'appleJuice'){
          this.appleJuiceCount = this.appleJuiceCount + count
        }else if(this.cheat === 'grapeJuice'){
          this.grapeJuiceCount = this.grapeJuiceCount + count
        }else if(this.cheat === 'money'){
          this.money = this.money + count
        }
        this.cheat = null;
        cheatingAudio.play();
    },
    completeOnlinOrder(){
      if(this.online === '1'){
          if(this.appleJuiceCount < this.apple1 || this.grapeJuiceCount < this.grape1){
            nopeAudio.play()
            alert(`You don't have enough items`)
          }else{
            this.appleJuiceCount = this.appleJuiceCount - this.apple1;
            this.grapeJuiceCount = this.grapeJuiceCount - this.grape1;
            this.money = this.money + this.odds1;
            honkAudio.play();
            setTimeout(this.delayedTrack, 900)
            setTimeout(this.delayedPaid, 3750)
            this.onlineOder();
          }
        }else if(this.online === '2'){
          if(this.appleJuiceCount < this.apple2 || this.grapeJuiceCount < this.grape2){
            nopeAudio.play()
            alert(`You don't have enough items`)
          }else{
            this.appleJuiceCount = this.appleJuiceCount - this.apple2;
            this.grapeJuiceCount = this.grapeJuiceCount - this.grape2;
            this.money = this.money + this.odds2;
            honkAudio.play();
            setTimeout(this.delayedTrack, 900)
            setTimeout(this.delayedPaid, 3750)
            this.onlineOder();
          }
        }else if(this.online === '3'){
          if(this.appleJuiceCount < this.apple3 || this.grapeJuiceCount < this.grape3){
            nopeAudio.play()
            alert(`You don't have enough items`)
          }else{
            this.appleJuiceCount = this.appleJuiceCount - this.apple3;
            this.grapeJuiceCount = this.grapeJuiceCount - this.grape3;
            this.money = this.money + this.odds3;
            honkAudio.play();
            setTimeout(this.delayedTrack, 900)
            setTimeout(this.delayedPaid, 3750)
            this.onlineOder();
            
          }
        }else if(this.online === '4'){
          if(this.appleJuiceCount < this.apple4 || this.grapeJuiceCount < this.grape4){
            nopeAudio.play()
            alert(`You don't have enough items`)
          }else{
            this.appleJuiceCount = this.appleJuiceCount - this.apple4;
            this.grapeJuiceCount = this.grapeJuiceCount - this.grape4;
            this.money = this.money + this.odds4;
            honkAudio.play();
            setTimeout(this.delayedTrack, 900)
            setTimeout(this.delayedPaid, 3750)
            this.onlineOder();
            
          }
        }
        else if(this.online === '5'){
          if(this.appleJuiceCount < this.apple5 || this.grapeJuiceCount < this.grape5){
            nopeAudio.play()
            alert(`You don't have enough items`)
          }else{
            this.appleJuiceCount = this.appleJuiceCount - this.apple5;
            this.grapeJuiceCount = this.grapeJuiceCount - this.grape5;
            this.money = this.money + this.odds5;
            honkAudio.play();
            setTimeout(this.delayedTrack, 900)
            setTimeout(this.delayedPaid, 3750)
            this.onlineOder();
            
          }
        }
        else if(this.online === '6'){
          if(this.appleJuiceCount < this.apple3 || this.grapeJuiceCount < this.grape6){
            nopeAudio.play()
            alert(`You don't have enough items`)
          }else{
            this.appleJuiceCount = this.appleJuiceCount - this.apple6;
            this.grapeJuiceCount = this.grapeJuiceCount - this.grape6;
            this.money = this.money + this.odds6;
            honkAudio.play();
            setTimeout(this.delayedTrack, 900)
            setTimeout(this.delayedPaid, 3750)
            this.onlineOder();
            
          }
        }
        this.online = null;
    },
    delayedPaid(){
      getPaidALotAudio.play()
    },
    delayedMarket(){
      spendAudio.play()
    },
    delayedTrack(){
      onlineOrderAudio.play()
    },
    buyMachine(price){
      if(this.money >= price){
        letmeseeAudio.play();
        this.checking = confirm(`Are you sure you want buy ${price}$ machine? You have ${this.money}$ now`)
        if(this.checking){
          this.money = this.money - price
          machineAudio.play();
          this.machineCount ++;
          this.onlineOder()
        }else{
        sighAudio.play()
        }
        
      }else{
        nopeAudio.play()
        alert(`You don't have enough money`)
      }
      
    },
    refresh(){
      if(this.money >= 5){
        this.money = this.money -5
        this.onlineOder();
      }else{
        nopeAudio.play()
      }
    },
    giveMoney(){
      this.num = Math.random()
      if(this.num <= 0.25){
        this.money = this.money + 0.25
      }else if(this.num <= 0.5){
        this.money = this.money + 0.5
      }else if(this.num <= 0.75){
        this.money = this.money + 0.75
      }else{
        this.money = this.money + 2
      }
      
    },
    freeMoney(price){
      this.money = this.money + price
    },
    makeDrink(num,price){
      if(this.mix === 'appleJuice'){
          if(this.appleCount < (num * price)){
            nopeAudio.play()
            alert(`You need ${num * price} apples!`)
          }else{
            this.appleCount = this.appleCount - (num * price)
            this.appleJuiceCount =this.appleJuiceCount + num
            pouringAudio.play();
          }
        }else if(this.mix === 'grapeJuice'){
          if(this.grapeCount < (num * price)){
            nopeAudio.play()
            alert(`You need ${num * price} grapes`)
          }else{
            this.grapeCount = this.grapeCount - (num * price)
            this.grapeJuiceCount = this.grapeJuiceCount + num
            pouringAudio.play();
          }
        }
        this.mix = null;
    },
    makeMaxDrink(){
      if(this.machineCount === 1){
        this.levelCal = 4
      }else if(this.machineCount === 2){
        this.levelCal = 3
      }else if(this.machineCount === 3){
        this.levelCal = 2
      }else if(this.machineCount === 4){
        this.levelCal = 1
      }else if(this.machineCount === 5){
        this.levelCal = 0.5
      }

      if(this.mix === 'appleJuice'){
        if(this.appleCount < this.levelCal ){
          nopeAudio.play();
          alert(`You need at least ${this.levelCal} apples!`)
        }else{
          this.MaxApple =  Math.floor(this.appleCount / this.levelCal)
          this.MaxConfirm =  confirm(`You are making ${this.MaxApple} apple juice out of ${this.MaxApple * this.levelCal} apples, do you want to continue?`)
          if(this.MaxConfirm){
            this.appleJuiceCount = this.appleJuiceCount + this.MaxApple
            this.appleCount = this.appleCount - (this.MaxApple * this.levelCal);
            pouringAudio.play();
          }else{  
            sighAudio.play();
          }
        }
      }else if(this.mix === 'grapeJuice'){
        if(this.grapeCount < this.levelCal ){
          nopeAudio.play();
          alert(`You need at least ${this.levelCal} grapes!`)
        }else{
          this.MaxGrape =  Math.floor(this.grapeCount / this.levelCal)
          this.MaxConfirm =  confirm(`You are making ${this.MaxGrape} apple juice out of ${this.MaxGrape * this.levelCal} apples, do you want to continue?`)
          if(this.MaxConfirm){
            this.grapeJuiceCount = this.grapeJuiceCount+ this.MaxGrape
            this.grapeCount = this.grapeCount - (this.MaxGrape * this.levelCal);
            pouringAudio.play();
          }else{  
            sighAudio.play();
          }
        }
      }
        this.mix = null;
    },
    onlineOder(){
      this.checkCount ++;
      this.randomOdds=  Math.random();
      if(this.randomOdds <= 0.4){
        this.randomOdds = 1.5
      }else if(this.randomOdds <= 0.8){
        this.randomOdds = 2
      }else if(this.randomOdds <= 0.95){
        this.randomOdds = 2.5
      }else {
        this.randomOdds = 4
      }

      if(this.machineCount === 1){
        this.levelCal = 4
      }else if(this.machineCount === 2){
        this.levelCal = 3
      }else if(this.machineCount === 3){
        this.levelCal = 2
      }else if(this.machineCount === 4){
        this.levelCal = 1
      }else if(this.machineCount === 5){
        this.levelCal = 0.5
      }

      this.randomNum = Math.random();
      this.apple1 = Math.floor((10 * this.randomNum) )
      this.grape1 = 10 - this.apple1;
      this.og1 = (this.apple1 * 3) + (this.grape1 * 5)
      this.odds1 = this.og1 * this.randomOdds
      this.cost1 = ((this.apple1 * 0.5) + (this.grape1 * 0.75)) * this.levelCal;
      this.pureProfit1 = this.odds1 - this.cost1;



      this.randomNum = Math.random();
      this.apple2 = Math.floor((50 * this.randomNum) )
      this.grape2 = 50 - this.apple2;
      this.og2 = (this.apple2 * 3) + (this.grape2 * 5)
      this.odds2 = this.og2 * this.randomOdds
      this.cost2 = ((this.apple2 * 0.5) + (this.grape2 * 0.75)) * this.levelCal;
      this.pureProfit2 = this.odds2 - this.cost2;



      this.randomNum = Math.random();
      this.apple3 = Math.floor((100* this.randomNum) )
      this.grape3 = 100 - this.apple3;
      this.og3 = (this.apple3 * 3) + (this.grape3 * 5)
      this.odds3 = this.og3 * this.randomOdds
      this.cost3 = ((this.apple3 * 0.5) + (this.grape3 * 0.75)) * this.levelCal;
      this.pureProfit3 = this.odds3 - this.cost3;

      this.randomNum = Math.random();
      this.apple4 = Math.floor((250 * this.randomNum) )
      this.grape4 = 250 - this.apple4;
      this.og4 = (this.apple4 * 3) + (this.grape4 * 5)
      this.odds4 = this.og4 * this.randomOdds
      this.cost4 = ((this.apple4 * 0.5) + (this.grape4 * 0.75)) * this.levelCal;
      this.pureProfit4 = this.odds4 - this.cost4;

      this.randomNum = Math.random();
      this.apple5 = Math.floor((500* this.randomNum) )
      this.grape5 = 500 - this.apple5;
      this.og5 = (this.apple5 * 3) + (this.grape5 * 5)
      this.odds5 = this.og5 * this.randomOdds
      this.cost5 = ((this.apple5 * 0.5) + (this.grape5 * 0.75)) * this.levelCal;
      this.pureProfit5 = this.odds5 - this.cost5;

      this.randomNum = Math.random();
      this.apple6 = Math.floor((1000* this.randomNum) )
      this.grape6 = 1000 - this.apple6;
      this.og6 = (this.apple6 * 3) + (this.grape6 * 5)
      this.odds6 = this.og6 * this.randomOdds
      this.cost6 = ((this.apple6 * 0.5) + (this.grape6 * 0.75)) * this.levelCal;
      this.pureProfit6 = this.odds6 - this.cost6;

      

      
    },
    catering(){
      if(this.money >= 2000){
        this.cateringCheck = confirm(`Do you want to unlock the online order with 2000$ ?`)
        if(this.cateringCheck){
          this.money = this.money - 2000;
          this.onlineOder()
          getPaidAudio.play()
            setTimeout(this.delayedPaid, 750)
            setTimeout(this.delayedPaid, 1500)
        }
        else{
          sighAudio.play();
        }
      }else{
        nopeAudio.play();
        alert(`You need 2000$ to unlock it!`)
      }
    }
  },
};
</script>

<style>
* {
  box-sizing: border-box;
}

html {
  font-family: sans-serif;
}

.buyList {
  border: 1px solid #0076bb;
  background-color: grey;
}
.chekDealButton{
  background-color: red;
  
}

.moneyButton{
  background-color: lightsalmon;
  color: black;
  
}

.refreshButton{
  background-color: lightslategray;
}

.toogleButton {
  border: 1px solid green;
  background-color: green;
}

body {
  margin: 0;
}
form {
  margin: 2rem auto;
  max-width: 40rem;
  border-radius: 12px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
  padding: 2rem;
  background-color: #ffffff;
}

.form-control {
  margin: 0.5rem 0;
}

.form-control.invalid input {
  border-color: red;
}

.form-control.invalid label {
  color: red;
}

label {
  font-weight: bold;
}

h2 {
  font-size: 1rem;
  margin: 0.5rem 0;
}

input,
select {
  display: block;
  width: 100%;
  font: inherit;
  margin-top: 0.5rem;
}

select {
  width: auto;
}

input[type='checkbox'],
input[type='radio'] {
  display: inline-block;
  width: auto;
  margin-right: 1rem;
}

input[type='checkbox'] + label,
input[type='radio'] + label {
  font-weight: normal;
}

button {
  font: inherit;
  border: 1px solid #0076bb;
  background-color: #0076bb;
  color: white;
  cursor: pointer;
  padding: 0.50rem 1rem;
  border-radius: 30px;
}

button:hover,
button:active {
  border-color: #002350;
  background-color: #002350;
}
</style>