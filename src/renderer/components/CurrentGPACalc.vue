<template>
  <div style="background-color: var(--color-background-soft); border-radius: 15px; padding: 20px">
    <h1 style="text-align: center">Current GPA Calculator</h1>
    <form>
      <div>
        <div v-for="(grade, index) in grades" :key="index" class="grade-row">
          <label v-if="index === 0" id="credit">Credits</label>
          <label v-if="index === 0" id="num-eq">Number Equivlent</label>
          <label v-if="index === 0" id="point-per-grade">Points per Grade</label>
          <label :for="grade" class="grade-label">{{ grade }}</label>
          <input
            :id="grade"
            v-model.number="gradeValues[grade]"
            type="number"
            step="1"
            min="0"
            required
            class="grade-input"
          />
          <input
            class="num-eq-box"
            readonly
            tabindex="-1"
            v-model.number="numEq[grade]"
            :style="{ backgroundColor: numEqColor[grade] }"
          />
          <input
            class="point-per-grade-box"
            :value="PointsPerGrade(grade)"
            readonly
            tabindex="-1"
          />
        </div>
        <br />
        <div class="output">
          <label style="grid-column-start: 1; grid-column-end: 2; text-align: left">
            Total Credits:
          </label>
          <input
            class="output-cell"
            :value="totalCredits"
            readonly
            tabindex="-1"
            style="grid-column-start: 2; grid-column-end: 3"
          />
          <label style="grid-column-start: 3; grid-column-end: 4; text-align: right"> GPA: </label>
          <input
            class="output-cell"
            :value="totalPoints"
            readonly
            tabindex="-1"
            style="grid-column-start: 4; grid-column-end: 5"
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
      },
      numEq: {
        A: 4.0,
        'A-': 3.7,
        'B+': 3.3,
        B: 3.0,
        'B-': 2.7,
        'C+': 2.3,
        C: 2.0,
        'C-': 1.7,
        'D+': 1.3,
        D: 1.0,
        F: 0
      },
      numEqColor: {
        A: '#1c522a',
        'A-': '#265429',
        'B+': '#385827',
        B: '#4c5d24',
        'B-': '#676021',
        'C+': '#684e22',
        C: '#684d22',
        'C-': '#683e23',
        'D+': '#683b23',
        D: '#692e24',
        F: '#692424'
      }
    }
  },
  computed: {
    totalPoints() {
      let result = 0
      let grades = this.grades
      for (let i = 0; i < grades.length; i++) {
        result += this.PointsPerGrade(grades[i])
      }
      return (result / this.totalCredits).toFixed(2)
    },
    totalCredits() {
      let result = 0
      let grades = this.grades
      for (let i = 0; i < grades.length; i++) {
        result += isNaN(parseInt(this.gradeValues[grades[i]]))
          ? 0
          : parseInt(this.gradeValues[grades[i]])
      }
      return result
    }
  },
  methods: {
    PointsPerGrade(grade) {
      return parseFloat(
        ((this.gradeValues[grade] * Math.floor(this.numEq[grade] * 10)) / 10).toFixed(1)
      )
    }
  }
}
</script>

<style scoped>
.grade-row,
.output {
  display: grid;
  grid-template-columns: 50px repeat(3, minmax(60px, 1fr));
  grid-gap: 1rem;
}
.grapde-label {
  grid-column-start: 1;
  grid-column-end: 2;
  margin-bottom: 1rem;
}

.grade-input,
.point-per-grade-box,
.num-eq-box,
.output-cell {
  height: 2.5rem;
  padding: 0 0.5rem;
  font-size: 1rem;
  border-radius: 15px;
  margin-bottom: 5px;
  background-color: var(--color-background-mute);
  border: none;
  color: var(--vt-c-text-dark-2);
  text-align: center;
}

.point-per-grade-box,
.num-eq-box:focus,
.output-cell {
  outline: none;
  pointer-events: none;
}

@keyframes border-pulse {
  0% {
    border-color: var(--vt-c-black-soft);
  }
  50% {
    border-color: var(--color-primary-200);
  }
  100% {
    border-color: var(--vt-c-black-soft);
  }
}

.grade-input:focus {
  outline: none;
  animation: border-pulse 2s infinite;
  border-bottom: 3px solid;
  background-color: var(--color-surface-mixed-250);
}

.grade-input {
  grid-column-start: 2;
  grid-column-end: 3;
  align-items: center;
}
.point-per-grade-box {
  grid-column-start: 4;
}

.num-eq-box {
  grid-column-start: 3;
  height: 2.5rem;
}

#credit {
  grid-column-start: 2;
  margin-bottom: 1rem;
  text-align: center;
}

#num-eq {
  grid-column-start: 3;
  margin-bottom: 1rem;
  text-align: center;
}

#point-per-grade {
  grid-column-start: 4;
  margin-bottom: 1rem;
  text-align: center;
}

input[type='number'].grade-input::-webkit-inner-spin-button,
input[type='number'].grade-input::-webkit-outer-spin-button {
  -webkit-appearance: none;
  appearance: none;
  background-color: transparent;
  margin: 0;
}
</style>
