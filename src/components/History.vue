<template>
  <div>
      <h3 class="history">History</h3>
      <button @click="saveToLog" class="btn btn-secondary">Save</button>
      <ul>
          <li v-for="(sum, index) in savedConversions" :key="sum.id" class="history">
              {{sum.inputAmount}}
              {{sum.name}}
              = {{sum.sum}} isk
              <button @click="remove(index)" class="btn history">x</button>

          </li>
      </ul>
  </div>
</template>

<script>
export default {
   props: ["objName", "objInput", "objResult"],
   data: () => {
     return {
         savedConversions: [],
     }
   },
   methods: {
     saveToLog(){
         let obj = {name: this.objName, inputAmount: this.objInput, sum: this.objResult, id: this.savedConversions.length}
         this.savedConversions.push(obj)
         console.log(this.calculation)
     },
     remove(index){
         this.savedConversions.splice(index, 1)
         console.log(index)
     }
   }
}
</script>

<style>
.history {
    color: greenyellow;
}
</style>