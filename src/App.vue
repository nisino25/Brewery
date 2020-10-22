<template>
  <base-container>
    <center>You have {{money}} $ now</center>
    <br>
    <center>
      Apple: {{appleCount}}, Grape: {{grapeCount}}, Water: {{WaterCount}}, Suger: {{SugerCount}}
      <br>
      Apple Juice: {{appleJuiceCount}}, Grape Juice: {{grapeJuiceCount}}
      <br>
      <br>
      <button @click="giveMoney"> Give me money</button>
      <button @click="freeMoney(10000)"> Free 10000</button>
      
    </center>
  </base-container>


  <base-container title="Market" >
    <button @click="toggleDisplayMarket" v-if="!MarketOpen"> +</button>
    <button @click="toggleDisplayMarket" v-else>-</button>
    <div v-if="MarketOpen">
      <br>
      <button @click="buyItem(2,'apple')">Apple(2 $)</button>
      <button @click="buyItem(3,'grape')">Grape(3 $)</button>
      <button @click="buyItem(1,'water')">Water(1 $)</button>
      <button @click="buyItem(0.5,'suger')">Suger(50 cents)</button>
    </div>
  </base-container>

  <base-container title="Factory" >
    <button @click="toggleDisplayFactory" v-if="!FactoryOpen"> +</button>
    <button @click="toggleDisplayFactory" v-else> -</button>
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
        <div>
          <button @click="makeDrink(1)">Make 1</button>
          <button @click="makeDrink(2)">Make 2</button>
          <br><br>
          <button v-if="machineCount === 1" @click="buyMachine(500)" class="buyList">Unlock the better machine(3 from 2!  500$)</button>
        </div>
      </form>
    </div>
  </base-container>


  <!-- I hide this section -->
  <base-container title="Storage" v-if="StorageOpen" >
  <button @click="toggleDisplayStorage" v-if="!StorageOpen"> +</button>
  <button @click="toggleDisplayStorage" v-else> -</button>
  </base-container>

  <base-container title="Store">
    <button @click="toggleDisplayStore" v-if="!StoreOpen"> +</button>
    <button @click="toggleDisplayStore" v-else> -</button>
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
    </div>
  </base-container>

</template>

<script>
import BaseContainer from './components/BaseContainer.vue';

// import TheForm from './components/TheForm.vue'
// import TheCounter from './components/TheCounter.vue';
// import ChangeCounter from './components/ChangeCounter.vue';
// import FavoriteValue from './components/FavoriteValue.vue';

var spendAudio = new Audio('/audio/spend.wav')
var getPaidAudio = new Audio('/audio/getPaid.wav')
var getPaidALotAudio = new Audio('/audio/getPaidAlot.wav')
var nopeAudio = new Audio('/audio/nope.m4a')
var pouringAudio = new Audio('/audio/pouring.mp3')
var letmeseeAudio = new Audio('/audio/hmm.wav')
var machineAudio = new Audio('/audio/machine.wav')
var sighAudio = new Audio('/audio/sigh.wav')




export default{
  data(){
    return{
      MarketOpen: false,
      FactoryOpen: false,
      StorageOpen: false,
      StoreOpen: false,
      money: 250,
      appleCount: 5,
      appleJuiceCount: 3,
      grapeCount: 5,
      grapeJuiceCount: 3,
      WaterCount: 2,
      SugerCount: 2,
      mix: null,
      sell: null,
      num : null,
      machineCount: 1,
      checking: false,
    }
  },
  components: {
    BaseContainer,
    // TheForm,
    // TheCounter,
    // ChangeCounter,
    // FavoriteValue,
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
    buyItem(price,item){
      if(this.money - price >= 0){
        this.money = this.money - price;
        if(item === 'apple'){
          this.appleCount++;
        }else if(item === 'grape'){
          this.grapeCount ++;
        }else if(item === 'water'){
          this.WaterCount++;
        }else if(item === 'suger'){
          this.SugerCount++;
        }
        spendAudio.play();
      }
      else{
        nopeAudio.play()
        alert("get your broke ass out this market")
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
    buyMachine(price){
      if(this.money >= price){
        letmeseeAudio.play();
        this.checking = confirm(`Are you sure you want buy ${price}$ machine? You have ${this.money}$ now`)
        if(this.checking){
          this.money = this.money - price
          machineAudio.play();
          this.machineCount ++;
        }else{
        sighAudio.play()
        }
        
      }else{
        nopeAudio.play()
        alert(`You don't have enough money`)
      }
      
    },
    giveMoney(){
      this.num = Math.random()
      if(this.num <= 0.25){
        this.money = this.money + 0.5
        
      }else if(this.num <= 0.5){
        this.money = this.money + 1
      }else if(this.num <= 0.75){
        this.money = this.money + 1.5
      }else{
        this.money = this.money + 2
      }
    },
    freeMoney(price){
      this.money = this.money + price
    },
    makeDrink(num){
      if(this.mix === 'appleJuice'){
          if(this.appleCount < num){
            nopeAudio.play()
            alert(`You don't have enough ingredients!`)
          }else{
            this.appleCount = this.appleCount - num
            this.appleJuiceCount =this.appleJuiceCount + num
            pouringAudio.play();
          }
        }else if(this.mix === 'grapeJuice'){
          if(this.grapeCount < num){
            nopeAudio.play()
            alert(`You don't have enough ingredients!`)
          }else{
            this.grapeCount = this.grapeCount - num;
            this.grapeJuiceCount = this.grapeJuiceCount + num
            pouringAudio.play();
          }
        }
        this.mix = null;
    },
    
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