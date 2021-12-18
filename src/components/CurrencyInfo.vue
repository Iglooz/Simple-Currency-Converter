<template>
  <div>
    <div class="container">
    <div v-if="isCurSet">
      <div class="row">
          <div class="col-lg-3"></div>
           <div class="d-flex p-2 curInfo col-6">
             <h3>{{currentIndex.longName}}</h3>
             
           </div>
           
           <div class="col-lg-3"></div>
        </div>
        <div class="row">
          <div class="col-lg-3"></div>
          <div class="col-6 curInfo">
            <p>1 {{currentIndex.shortName}} = {{currentIndex.value}} isk </p>
          </div>
          <div class="col-lg-3"></div>
        </div>
      </div>
    <div v-if="!isCurSet" class="d-flex p-2 curInfo col-6">
           <p>Select a currency from the list below</p>
    </div>

      
    </div>
    
    
    <div>
      <ul>
        <li v-for="cur in Currency.results" class="btn btn-secondary curOptions" :class="{selected: cur == isCurSet}" :key="cur" @click="emitExchangeValue(cur)">{{cur.shortName}}</li>
      </ul>
    </div>

  </div>
</template>

<script>
export default {
 props: ['Currency'],
data: () => {
  return {
    isCurSet: undefined,
    currentIndex: undefined,
  }
},
methods: {
    emitExchangeValue(exRate){
      this.isCurSet = exRate
      this.currentIndex = exRate
      this.$emit('getConversionRate', exRate.value)
      console.log(exRate.value)
    }
}

}
</script>

<style scoped>
li {

  list-style: none;
  text-align: center;
  background-color: #858585;
  margin-right: 10px;
  margin-bottom: 10px;
  width: 100px;
  height: 100px;
  line-height: 60px;
  border: 10px;
  border-color: black;
  display: inline-block;
}
.selected {
  color: greenyellow;
  background-color: rgb(192, 189, 189);
  
}
.curInfo {
  background-color: black;
  color: greenyellow;
  max-width: 30%;
  margin: 1%;
}
.curOptions {
  
}

</style>