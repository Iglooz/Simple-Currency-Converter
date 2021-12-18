<template>
  <div id="app">
    <!--Currency source selector-->
    <header>
      <div class="currencySourceSelection">
        <button @click="setSourceM5" class="btn btn-primary">M5</button>
        <button @click="setSourceArion" class="btn btn-primary">Arion</button>
        <span>
          <p class="greenText">source: {{ exchangeSourceName }}</p>
        </span>
      </div>
    </header>
    <div class="container align-items-center">
      <!--Displays the calculated result-->
      <div class="row">
        <div class="col-lg-3"></div>
        <div class="col-6 moneyArea d-flex p-2">
          <Conversion
            :amount="inputValue"
            :conversionRate="exchangeRate"
            v-on:calculatedSum="getCalculatedSum($event)"
          />
        </div>
        <div class="col-lg-3"></div>
      </div>
      <!--User input field -->
      <div class="row">
        <div class="col-3"></div>
        <div class="col-6 inputArea d-flex p-2 form-group">
          <input
            type="number"
            v-model="inputValue"
            class="valueInput form-control"
          />
        </div>
        <div class="col-3"></div>
      </div>
      <!--Currency selection and information-->
      <div class="row">
        <div class="col-l-7 col-xs">
          <CurrencyInfo
            :Currency="exchangeRateSource"
            v-on:getConversionRate="updateExchangeRate($event)"
            v-on:getCurrencyName="getCurrentCurrencyName($event)"
          />
        </div>
      </div>
      <!--Displays a list of saved calculations-->
      <div class="row">
        <div class="col">
          <History
            :objName="currentName"
            :objInput="inputValue"
            :objResult="calculatedSum"
          />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Conversion from "./components/Conversion.vue";
import CurrencyInfo from "./components/CurrencyInfo.vue";
import History from "./components/History.vue";
import axios from "axios";

export default {
  name: "App",
  components: {
    Conversion,
    CurrencyInfo,
    History,
  },
  data: () => {
    return {
      exchangeRateSource: [],
      exchangeSourceName: "M5",
      inputValue: 0,
      exchangeRate: 0,
      currentName: undefined,
      calculatedSum: 0,
      calculationObj: {},
    };
  },
  methods: {
    // Sets the currency information sources
    setSourceM5() {
      axios
        .get("https://apis.is/currency/m5")
        .then((resp) => {
          this.exchangeRateSource = resp.data;
          console.log(resp);
        })
        .catch((error) => console.log(error));
      this.exchangeSourceName = "M5";
    },
    setSourceArion() {
      axios
        .get("https://apis.is/currency/arion")
        .then((resp) => {
          this.exchangeRateSource = resp.data;
          console.log(resp);
        })
        .catch((error) => console.log(error));
      this.exchangeSourceName = "Arion";
    },
    // Updates the exchange rate whenever a new currency is selected
    updateExchangeRate(value) {
      this.exchangeRate = value;
      console.log(value);
    },
    // Gets the values required to send as a prop to the history component
    getCurrentCurrencyName(name) {
      this.currentName = name;
      console.log(name);
    },
    getCalculatedSum(value) {
      this.calculatedSum = value;
      console.log(value);
    },
  },
  computed: {},
  mounted() {
    axios
      .get("https://apis.is/currency/m5")
      .then((resp) => {
        this.exchangeRateSource = resp.data;
        console.log(resp);
      })
      .catch((error) => console.log(error));
  },
};
</script>

<style>
* {
  background-color: black;
  font-family: "Chakra Petch";
}
.valueInput {
  max-width: 500px;
}
.greenText {
  color: greenyellow;
}
.currencySourceSelection {
  margin-left: 2%;
}
@import url("https://fonts.googleapis.com/css2?family=Chakra+Petch:wght@400;700&display=swap");
</style>

