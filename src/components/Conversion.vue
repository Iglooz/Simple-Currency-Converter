<template>
  <div>
    <!--Displays the computed result of the user input and exchange rate-->
    <div class="row">
      <div class="col-6">
        <div class="iskDisplay">
          <h1 class="iskDisplay">{{calculateToIsk}} <span class="iskSmall">ISK</span> </h1>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["amount", "conversionRate"],
  data: () => {
    return {
      
    };
  },
  methods: {
    
  },
  watch: {
     calculateToIsk: function(){
      let sum = undefined
      sum = this.calculateToIsk
      this.$emit('calculatedSum', sum)
    }
  },
  computed: {
    // Returns the computed result of the user input and exchange rate
    calculateToIsk() {
      return Math.round(this.amount * this.conversionRate);
    },
  },
};
</script>

<style>
.iskDisplay {
  margin-top: 10%;
  text-align: center;
  font-family: "Chakra Petch";
  color: greenyellow;
  font-size: 200%;
  min-height: 100px;
  min-width: 450px;
}
.iskSmall {
  font-size: 100% !important;
}
</style>