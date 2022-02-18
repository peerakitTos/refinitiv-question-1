<template>
  <div class="d-flex" style="min-width: 600px;">
    <div style="width: 200px">
      <input type="number" style="border: 1px solid #000" v-model="inputVal" min="1" @input="handleInput" />
    </div>
    <div style="min-width: 100px; flex: 1 0 auto">
      <v-select
        v-model="selectVal"
        style="border: 1px solid #000; max-width: 100px;"
        class="ma-0 pa-0"
        :items="options"
        item-value="value"
        item-text="text"
        hide-details
      >
      </v-select>
    </div>
    <div style="width: 300px">{{ answer }}</div>
  </div>
</template>

<script>
export default {
  name: "IndexPage",
  data() {
    return {
      inputVal: 2,
      selectVal: "isPrime",
      options: [
        {
          text: "isPrime",
          value: "isPrime",
        },
        {
          text: "isFibonacci",
          value: "isFibo",
        },
      ],
      fibonacciArray: [1, 2]
    };
  },
  computed: {
    answer() {
      if (this.selectVal === "isPrime") {
        return this.isPrimeCalculation();
      }
      return this.isFibonacciCalculation();
    },
  },
  methods: {
    handleInput(e) {
      if(e.target.value < 0) {
        this.inputVal = 1
        return
      }
      this.inputVal = e.target.value
    },
    isPrimeCalculation() {
      if(this.inputVal < 2) {
        return false
      }
      for(let i = 2; i <= Math.floor(this.inputVal / 2); i++) {
        if(this.inputVal % i === 0) {
          return false
        }
      }
      return true
    },
    isFibonacciCalculation() {
      while(parseFloat(this.inputVal) > this.fibonacciArray[this.fibonacciArray.length - 1]) {
        const lastVal = this.fibonacciArray[this.fibonacciArray.length - 1]
        const beforeLastVal = this.fibonacciArray[this.fibonacciArray.length - 2]
        const newFibo = lastVal + beforeLastVal
        this.fibonacciArray.push(newFibo)
      }
      if(this.fibonacciArray.indexOf(parseFloat(this.inputVal)) !== -1) {
        return true
      }
      return false;
    },
  },
};
</script>
