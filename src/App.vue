<template>
  <div id="app">
    
    
    
    <div class="container align-items-center">
      <div class="row">
        <div class="col-lg-3"></div>
        <div class="col-6 moneyArea d-flex p-2">
          <Conversion :amount="inputValue" :conversionRate="exchangeRate" />
        </div>
        <div class="col-lg-3"></div>
        
      </div>
        <div class="row">
          <div class="col-3"></div>
            <div class="col-6 inputArea d-flex p-2 form-group">
               <input type="number" :key="input" v-model="inputValue" class="valueInput form-control">
            </div>
          <div class="col-3"></div>
        </div>
        <div class="row">
          <div class="col-l-7 col-xs">
             <CurrencyInfo :Currency="exchangeRateSource" v-on:getConversionRate="updateExchangeRate($event)"/>
          </div>
          
        
          
        </div>

        <div class="row">
          <div class="col">
            
            <button @click="setSourceM5" class="btn btn-primary">M5</button>
            <button @click="setSourceArion" class="btn btn-primary">Arion</button>
            <span>
              <p class="greenText">Current source: {{exchangeSourceName}}</p>
            </span>
            
          </div>
        </div>

    </div>

    

  </div>
</template>

<script>
import Conversion from './components/Conversion.vue'
import CurrencyInfo from './components/CurrencyInfo.vue'
import axios from 'axios'


export default {
  name: 'App',
  components: {
    Conversion,
    CurrencyInfo,
  },
  data: () => {
    return{
      exchangeRateSource: [],
      exchangeSourceName: 'M5',
      inputValue: 0,
      exchangeRate: 0,
    }
    
  

  },
  methods: {
     test(){
      console.log(this.exchangeRate)
      console.log(this.inputValue)
      
    },
    setSourceM5(){
        axios.get('https://apis.is/currency/m5').then(resp =>{
        this.exchangeRateSource = resp.data
        console.log(resp)

      }).catch(error => console.log(error))
      this.exchangeSourceName = 'M5'
      console.log(this.setDataM5)
      console.log(this.exchangeRateSource)
    },
    setSourceArion(){
      axios.get('https://apis.is/currency/arion').then(resp =>{
        this.exchangeRateSource = resp.data
        console.log(resp)

      }).catch(error => console.log(error))
      this.exchangeSourceName = 'Arion'
      console.log(this.setDataArion)
      console.log(this.exchangeRateSource)

    },
    updateExchangeRate(value){
      this.exchangeRate = value
      console.log(value)
    }
  },
  computed: {
    
  },
  mounted() {
      
        axios.get('https://apis.is/currency/m5').then(resp =>{
        this.exchangeRateSource = resp.data
        console.log(resp)

      }).catch(error => console.log(error))
    
  }
}
</script>

<style>
* {
  background-color: black;
  font-family: 'Chakra Petch';
}
.valueInput {
  max-width: 500px;
}
.moneyArea {
  
}
.greenText {
  color: greenyellow
}
@import url('https://fonts.googleapis.com/css2?family=Chakra+Petch:wght@400;700&display=swap');
</style>

