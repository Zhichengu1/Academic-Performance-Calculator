<template>
  <div>
    <h1 style = "text-align: center" >Future GPA Calculator</h1>
    <form @submit.prevent="calculateGPA">
    <table>
    <tr>
      <td style = "color:black; background-color: lightgray;">I. Total credits used to calculate your cumulative GPA</td>
    </tr>
    <tr v-for="(label, index) in labels" :key="index">
      <td><input :id="'input' + index" v-model.number="inputs['input' + index]" type="number" min="0" required /></td>
      <td>{{ label }}</td>
    </tr>
    <tr>
      <td>output</td>
      <td>Total GPA credits*</td>
    </tr>
    </table>
    <h2 style ="text-align: center">Calculate Your cumulative GPA</h2>
    <div class ="grid-columns">
    <div v-for = "(label, index) in labels_gpa" :key="index">
      <label for = "'input' + index"> {{label}} </label>
      <input :id = "'input' + index" v-model.number = "inputs['input' + index]" type="number" min="0" required />
    </div>
  </div>

    </form>
    <p v-if="result !== null">Your current GPA is: {{ result }}</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      labels: [':Enter TOTAL earned credits:', ':Enter repeated credits NOT earned.', ':Enter TOTAL credits of F, I/F, and N/F grades', ':Enter TOTAL credits of P and S grades', ':Enter TOTAL transfer and test(AP, CLEP, CPE) creidts'],
      inputs: {},
      labels_gpa: ['Current GPA credits: ', 'Current quality Points:', 'display', 'Anticipated credits:', 'Future quality points:', 'Display', 'Overall credits:', 'Total Quatlity points', 'Display'],
      gpa: null,
      earn_credits: null,
      total_credit: null,
      result: null
    }
  },
  methods: {
    calculateGPA() {
      this.result = this.gpa
    },
    calculateCredit()
    {
      this.total_credit = this.earn_credits
    }
  }
}
</script>

<style>
input,
input:hover
{
  width: auto;
  height: 35px;
  background-color: darkseagreen	;
  border-color: transparent;
}
.grid-columns {
    display: grid; 
    grid-template-columns: repeat(3, 1fr); /* Change this line */
}
table
{
  border: 2px solid blueviolet;
  border-width: auto;
}

input[type="number"]::-webkit-inner-spin-button, 
input[type="number"]::-webkit-outer-spin-button { 
  -webkit-appearance: none; 
}

/*  


<div class = "calculateGPA">
      <button type="submit">Calculate</button>
        <div  v-for = "(label, index) in labels_gpa" :key="index">
          <label: for = "'input' + index"> {{label}} </label:>
          <input :id = "'input' + index" v-model.number = "inputs['input' + index]" type="number" min="0" required />
        </div>
      </div>*/

</style>
