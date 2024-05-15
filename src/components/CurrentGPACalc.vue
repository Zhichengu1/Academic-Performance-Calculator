<template>
  <div>
    <h1>Current GPA Calculator</h1>
    <form>
      <div class="grade-row">
        <label id="credit">Total Credits</label>
        <div v-for="(grade, index) in grades" :key="index" class="grade-input">
          <label :for="grade">{{ grade }}:</label>
          <input
            :id="grade"
            v-model.number="gradeValues[grade]"
            type="number"
            step="1"
            min="0"
            required
          />
        </div>
      </div>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      grades: ['A', 'A-', 'B+', 'B', 'B-', 'C+', 'C', 'C-', 'D+', 'D', 'F'],
      gradeValues: {
        A: 0,
        'A-': 0,
        'B+': 0,
        B: 0,
        'B-': 0,
        'C+': 0,
        C: 0,
        'C-': 0,
        'D+': 0,
        D: 0,
        F: 0
      }
    }
  }
}
</script>

<style scoped>
.grade-row {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
}

.grade-input {
  display: flex;
  justify-content: space-between;
  width: 100%;
  margin-bottom: 1rem;
}

#credit {
  margin-bottom: 1rem;
  margin-left: auto;
}
</style>
