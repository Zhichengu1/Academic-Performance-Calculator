<template>
  <div class = "page_layout">
    <h1 style = "text-align: center;">Future GPA Calculator</h1>
    <form @submit.prevent="calculateGPA">
    <table>
    <tr>
      <td style = "color:black; background-color: lightgray; border-radius: 15px;">I. Total credits used to calculate your cumulative GPA</td>
    </tr>
    <tr v-for="(label, index) in labels" :key="index">
      <td><input class = "animation" :id="'credit_input' + index" v-model.number="credit_input['credit_input' + index]" type="number" min="0" required /></td>
      <td>{{ label }}</td>
    </tr>
    <tr>
      <td>output</td>
      <td>Total GPA credits*</td>
    </tr>
    </table>
    <div style = "color:black; background-color: lightgray; border-radius: 15px; margin-right: 500px;">II. Calculating Your Cumulative GPA</div>
    <div class ="grid-columns">
    <div v-for = "(label, index) in labels_gpa" :key="index">
      <label for = "'gpa_input' + index"> {{label}} </label>
      <input :id = "'gpa_input' + index" v-model.number = "gpa_input['gpa_input' + index]" type="number" min="0" required />
    </div>
    </div>
  </form>
  </div>
<p v-if="result !== null">Your current GPA is: {{ result }}</p>
</template>
<script>
export default {
  data() {
    return {
      labels: [':Enter TOTAL earned credits:', ':Enter repeated credits NOT earned.', ':Enter TOTAL credits of F, I/F, and N/F grades', ':Enter TOTAL credits of P and S grades', ':Enter TOTAL transfer and test(AP, CLEP, CPE)'],
      credit_input: {},
      labels_gpa: 
      [
        'Enter current GPA credits:', 
        'Enter current quality points:', 
        'Display current GPA:', 
        'Enter anticipated credits:', 
        'Enter future quality points:', 
        'Display future GPA:', 
        'Enter overall credits:', 
        'Enter total quality points', 
        'Display overall GPA'
      ],
      gpa_input: {},
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
input
{
  width: auto;
  height: 35px;
  background-color: var(--color-background-mute);
  color: var(--vt-c-text-dark-2);
  border-color: transparent;
}
input:hover
{
  animation: pulse 3s infinite;
}
.grid-columns { 
    display: grid; 
    grid-template-columns: repeat(3, 1fr); /* Change this line */
}
table
{
  border-width: auto;
  padding-bottom: 1rem;
  padding-top: 1rem;
}
input[type="number"]::-webkit-inner-spin-button, 
input[type="number"]::-webkit-outer-spin-button { 
  -webkit-appearance: none; 
}
.page_layout
{
  border-radius: 15px;
  font-size: 1rem;
  border-width: auto;
  margin-bottom: 5px; 
  padding: 20px;  
  background-color: var(--color-background-soft); 
  border: outset;
  animation: pulse 10s infinite;
}
@keyframes pulse {
  0%, 100% {
    border-color: black; /* Light Gray */
  }
  30% {
    border-color: #A9A9A9; /* Dark Gray */
  }
  50% {
    border-color: #808080; /* Gray */
  }
  70% {
    border-color: #696969; /* Dim Gray */
  }
}
</style>
