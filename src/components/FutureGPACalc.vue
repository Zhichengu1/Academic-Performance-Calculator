<template>
  <div>
    <h1 style = "text-align: center" >Future GPA Calculator</h1>
    <form @submit.prevent="calculateGPA">

      <div class = "table">
        <div v-for = "(label, index) in labels" :key="index">
          <label: for = "'input' + index"> {{label}} </label:>
          <input :id = "'input' + index" v-model.number = "inputs['input' + index]" type="number" min="0" required />
        </div>
      </div>
      <div class = "calculateGPA">
        <div v-for = "(label, index) in labels_gpa" :key="index">
          <label: for = "'input' + index"> {{label}} </label:>
          <input :id = "'input' + index" v-model.number = "inputs['input' + index]" type="number" min="0" required />
        </div>
      </div>
      <button type="submit">Calculate</button>
    </form>
    <p v-if="result !== null">Your current GPA is: {{ result }}</p>
  </div>
</template>


<script>
export default {
  data() {
    return {
      labels: ['Total Credits:', 'Credits of F, I/F, and N/F Grade:', 'Credits of P and S:', 'Total transfer and Test:'],
      labels_gpa: ['Current quality Points:', 'Anticipated credits:', 'Future quality points:'],
      inputs: {},
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
  border-radius: 30px;
  width: 80px;
  height: 35px;
  background-color: lightgray;
  border-color: transparent;
}
input:hover
{
  background-color: lightslategray;
}
.calculateGPA
{
  text-align: right;
}

.table
{
  display: grid;
  grid-template-columns: auto auto auto auto; /* Creates four columns */
  grid-template-rows: auto;
}


input[type="number"]::-webkit-inner-spin-button, 
input[type="number"]::-webkit-outer-spin-button { 
  -webkit-appearance: none; 
}


</style>
