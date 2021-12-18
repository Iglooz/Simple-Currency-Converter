<template>
  <div>
        <!--Displays the selected currency information or prompts the user to select one-->
    <div class="container">
      <div v-if="isCurSet">
        <div class="row">
          <div class="curInfo col-6">
            <h3>{{ currentIndex.longName }}</h3>
          </div>
        </div>
        <div class="row">
          <div class="col-6 curInfo">
            <p>1 {{ currentIndex.shortName }} = {{ currentIndex.value }} isk</p>
          </div>
        </div>
      </div>
      <div v-if="!isCurSet" class="curInfo col-6">
        <p>Ekkert valið</p>
      </div>
    <div>
      <!--Shows the available currency options from the api -->
      <div>
        <ul>
          <li
            :key="cur.id"
            v-for="cur in Currency.results"
            class="btn btn-secondary curOptions"
            :class="{ selected: cur == isCurSet }"
            @click="emitExchangeValue(cur)"
          >
            {{ cur.shortName }}
          </li>
        </ul>
      </div>
    </div>

    </div>
  </div>
</template>

<script>
export default {
  props: ["Currency"],
  data: () => {
    return {
      isCurSet: undefined,
      currentIndex: undefined,
    };
  },
  methods: {
    // Emits the currently selected currencies exchange rate to the main file, also handles the bool state of a selected currency
    emitExchangeValue(exRate) {
      this.isCurSet = exRate;
      this.currentIndex = exRate;
      this.$emit("getConversionRate", exRate.value);
      this.$emit("getCurrencyName", exRate.longName);
      console.log(exRate.value);
    },
  },
};
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
  margin-left: 10%;
}
.curOptions {
}
</style>