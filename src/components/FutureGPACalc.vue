<template>
  <div class = "page_layout">
    <h1 style = "text-align: center;">Future GPA Calculator</h1>
    <form @submit.prevent="calculateGPA">
    <table>
    <tr>
      <td style = "color: lightsteelblue; background-color: var(--color-background-mute); border-radius: 15px;">I. Total credits used to calculate your cumulative GPA</td>
    </tr>
    <tr v-for="(label, index) in labels" :key="index">
      <td><input class = "animation" :id="'credit_input' + index" placeholder="0" v-model.number="credit_input[index]" type="number" min="0" required /></td>
      <td>{{ label }}</td>
    </tr>
    <tr>
      <td class ="display_total">{{calculateCredit()}}</td>
      <td>:Total Earned GPA Credits*</td>
    </tr>
    </table>
    <div style = "color:lightsteelblue; background-color: var(--color-background-mute); border-radius: 15px; margin-right: 500px;">II. Calculating Your Cumulative GPA</div>
    <div class ="grid-columns">
    <div v-for = "(label, index) in labels_gpa" :key="index">
      <label for = "'gpa_input' + index"> {{label}} </label>
      <input v-if = "index == 1 || index == 3 || index ==4 " :id = "'gpa_input' + index" placeholder="0" v-model.number = "gpa_input[index]" type="number" min="0" required />
      <input v-else  :id = "'gpa_input' + index" placeholder="0" :value = "calculatedGPA[index]" type="number" min="0" style="border: outset; animation: credit_pal 3s infinite" disabled/>
    </div>
  </div>
  <div class ="final_result">  
    <p v-if="total_credit !== null">Your Anticipated GPA is: {{ anticipatedGpa() }}</p>
  </div>
  </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      labels: [':Enter TOTAL earned credits:', ':Enter repeated credits NOT earned.', ':Enter TOTAL credits of F, I/F, and N/F grades', ':Enter TOTAL credits of P and S grades', ':Enter TOTAL transfer and test(AP, CLEP, CPE)'],
      credit_input: [0,0,0,0,0],
      labels_gpa: 
      [
        'Current GPA credits:', 
        'Enter current quality points:', 
        'Display current GPA:', 
        'Future credits:', 
        'Enter Future quality points:', 
        'Display Future GPA:', 
        'Overall credits:', 
        'Total quality points:', 
        'Display overall Quality Point:'
      ],
      gpa_input: [0, 0, 0, 0, 0, 0, 0, 0, 0],
      total_credit: 0,
      anticipated_gpa: 0,
      credit_8: 0,
      grade_6: 0
    }
  },
  computed: {
    calculatedGPA() {
      return this.labels_gpa.map((label, index) => 
      {
        let result = 0;
        switch(index) {
          case 0:
            result = this.calculateCredit() + this.gpa_input[4];
            this.gpa_input[0] = result;
            this.grade_6 = result;
            break;
          case 6:
            result = this.gpa_input[0] + this.gpa_input[3];
            this.gpa_input[6] = result;
            break;
          case 2:
            result = this.gpa_input[0] * this.gpa_input[1];
            this.gpa_input[2] = result;
            this.credit_8 = result;
            break;
          case 5:
            result = this.gpa_input[3] * this.gpa_input[4];
            this.gpa_input[5] = result;
            break;
          case 8:
            result = this.gpa_input[2] + this.gpa_input[5];
            this.gpa_input[8] = result;
            break;
          default:
            result = this.gpa_input[1] * this.gpa_input[4];
    }
    return result;});
}
  },
  methods: {
    calculateCredit()
    {
      let total_credit = this.credit_input[0]+ this.credit_input[1]+ this.credit_input[2] - this.credit_input[3] - this.credit_input[4];
      if(total_credit < 0)
      {
        return "Total credit can not be negative.";
      }
      return total_credit;
    },
    anticipatedGpa()
    {
      return this.gpa_input[8]/this.gpa_input[6];
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
  text-align: center;
}
.display_total
{
  width: auto;
  height: 35px;
  color: var(--vt-c-text-dark-2);
  text-align: center;
  background-color: var(--color-background-soft); 
  border:outset;
  animation: credit_pal 3s infinite;
}
input:hover
{
  animation: pulse 3s infinite;
}
.grid-columns { 
    display: grid; 
    grid-template-columns: repeat(3, 1fr); /* Change this line */
    padding-bottom:20px;
}
table
{
  border-width: auto;
  padding-bottom: 1rem;
  padding-top: 1rem;
}
.final_result
{
  border: 2px outset;
  animation: credit_pal 3s infinite;
  text-align: center;
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
@keyframes credit_pal
{
  0%, 50% {
    border-color: #556B2F;
  }
   30% {
    border-color: #98FB98;
  }
  50% {
    border-color: #8FBC8F;
  }
}
</style>
