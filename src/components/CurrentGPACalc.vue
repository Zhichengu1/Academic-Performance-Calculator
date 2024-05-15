<template>
  <div>
    <h1>Current GPA Calculator</h1>
    <form>
      <div>
        <div v-for="(grade, index) in grades" :key="index" class="grade-row">
          <label v-if="index === 0" id="credit">Total Credits</label>
          <label v-if="index === 0" id="num-eq">Number Equivlent</label>
          <label v-if="index === 0" id="point-per-grade">Points per Grade</label>
          <label :for="grade" class="grade-label">{{ grade }}:</label>
          <input
            :id="grade"
            v-model.number="gradeValues[grade]"
            type="number"
            step="1"
            min="0"
            required
            class="grade-input"
          />
          <input class="num-eq" readonly />
          <input class="point-per-grade" readonly />
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
  display: grid;
  grid-template-columns: 50px repeat(auto-fill, minmax(200px, 1fr));
  grid-gap: 0.5rem;
}
.grapde-label {
  grid-column-start: 1;
  grid-column-end: 2;
  margin-bottom: 1rem;
}
.grade-input {
  grid-column-start: 2;
  grid-column-end: 3;
  align-items: center;
}
.point-per-grade {
  grid-column-start: 4;
}

.num-eq {
  grid-column-start: 3;
  height: 2.5rem;
}

#credit {
  grid-column-start: 2;
  margin-bottom: 1rem;
}

#num-eq {
  grid-column-start: 3;
  margin-bottom: 1rem;
}

#point-per-grade {
  grid-column-start: 4;
  margin-bottom: 1rem;
}
</style>
