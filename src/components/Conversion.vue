<template>
  <div>
    <div class="row">
      <div class="col-6">
        <div class="iskDisplay"> 
          <h1 class="iskDisplay">{{calculateToIsk}} ISK</h1>
        </div>
      </div>
    </div>
      
      
    
    

  </div>
</template>

<script>
export default {
  props: ['amount', 'conversionRate'],
data: () => {
return {

}
},
methods: {
  
},
computed: {
  calculateToIsk(){
    return this.amount * this.conversionRate
  }
}
}
</script>

<style>
.iskDisplay {
  text-align: center;
  font-family: 'Chakra Petch';
  color: greenyellow;
  font-size: 200%;
  min-height: 100px;
  min-width: 450px;
  
}
</style>