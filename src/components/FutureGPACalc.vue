<template>
  <div>
    <h1 style = "text-align: center" >Future GPA Calculator</h1>
    <form @submit.prevent="calculateGPA">
      <div>
        <label for="gpa">Future GPA:</label>
        <input id="gpa" v-model.number="gpa" type="number" step="0.01" min="0" max="4" required />
      </div>
      <div>
        <label for="credits">Total Credits:</label>
        <input id="credits" v-model.number="credits" type="number" min="0" required />
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
      gpa: null,
      credits: null,
      result: null
    }
  },
  methods: {
    calculateGPA() {
      this.result = this.gpa
    }
  }
}
</script>
