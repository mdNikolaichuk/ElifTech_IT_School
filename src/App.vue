<template>
  <div id="app">
    <h1>Mortage calculator</h1>
    <img src="../public/file.png" alt=""> <br>  
    <p>Select bank</p>
    <select name="" id="bank">
      <option v-for="bank in bankList" :key="bank" :value="bank.name">
        {{ bank.name }}
      </option>
    </select>
    <br>
    <p>Write initial loan</p>
    <input
      id="loanInp"
      type="number"
      placeholder="Initial loan"
      v-model="iLoan"
    /> <br>
    <p>How long?</p> 
    <input
      type="number"
      name="term"
      id="term"
      placeholder="Loan term"
      v-model="lTerm"
    /> <br> <br>
    <button @click="print()">Calculate</button>
    <hr />
    <ul v-for="res in result" :key="res">
      {{
        res
      }}
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      bankList: [
        {
          name: "bank1",
          rate: 0.5,
          maxLoan: 300000,
        },
        {
          name: "bank2",
          rate: 1,
          maxLoan: 100000,
        },
        {
          name: "bank3",
          rate: 2,
          maxLoan: 500000,
        },
      ],
      loanTerm: 0,
      minPay: 0,
      result: [],
      iLoan: 0,
      lTerm: 0,
    };
  },
  methods: {
    print() {
      var rate = 0;
      this.result = []
      for (var i = 0; i <= this.bankList.length; i++) {
        if (this.bankList[i].name == document.getElementById("bank").value) {
          rate = this.bankList[i].rate;
          if (this.bankList[i].maxLoan < this.iLoan) {
            this.result[0] = "The bank does not have the required amount";
          } else {
            for (let index = 1; index < this.lTerm; index++) {
              this.result.push(
                ((this.iLoan * (rate / 12)) * (Math.pow((1 + rate / 12), index))) /
                  (Math.pow((1 + rate / 12), index) - 1)
                
              );
              
            }
          }
        }
      }
    },
  },
};
</script>

<style>
body{
  background-color: burlywood;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;

}
</style>
