<template>
  <div>
    <h1 style = "text-align: center" >Future GPA Calculator</h1>
    <form @submit.prevent="calculateGPA">
      <div class = "total_credit">
        <div v-for = "(label, index) in labels" :key="index">
          <label: for = "'input' + index"> {{label}} </label:>
          <input :id = "'input' + index" v-model.number = "inputs['input' + index]" type="number" min="0" required />
        </div>
      </div>

      <div>

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
      labels: ['Total Credits:', 'Credits of F, I/F, and N/F Grade', 'Credits of P and S Grades', 'Total transfer and Test'],
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

.total_credits
{
  text-align: left;
}

.calculateGPA
{
  text-align: right;
}



</style>
