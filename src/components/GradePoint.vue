<template>
  <section class="grade p-2 px-4 sm:px-4 sm:p-4">
    <h1 class="text-4xl sm:text-6xl font-bold headingFont text-center">
      Welcome to GPA Buddy.
    </h1>
    <p class="textFont mb-3 sm:text-2xl text-xl">
      Using GPA Buddy, you can easily calculate grade point average.
    </p>
    <form action="">
      <div class="grade__form-control mx-auto sm:w-1/2 w-full" v-if="start">
        <app-button title="Get Started">
          <button
            @click.prevent="startCalculator"
            :class="['btn--yellow']"
            class=" btn inline-block text-white rounded px-4 py-4 sm:text-xl  font-bold text-center text-2xl font-textFont shadow-xl w-full  mx-auto my-6"
          >
            {{ startTitle }}
          </button>
        </app-button>
      </div>

      <div class="" v-if="process">
        <div
          class="form-control flex justify-center items-center"
          v-for="(data, index) in formData"
          :key="index"
        >
          <div class="grade__form-group">
            <label :for="count" class="font-bold">Course</label>
            <input
              type="text"
              class="textFont py-2 px-1 sm:px-4 rounded grade__input mb-3"
              v-model="data.course"
            />
          </div>

          <div class="ml-2 sm:ml-4 grade__form-group">
            <label :for="count" class="grade__form-group font-bold"
              >Grade</label
            >
            <select
              type="text"
              class="textFont py-2 px-1 sm:px-4 rounded grade__input mb-3 grade__input-select"
              v-model="data.grade">
              <option selected>A</option>
              <option v-for="(grade, index) in grades" :key="index">
                {{ grade }}
              </option>
            />
            </select>
          </div>
          <div class="ml-2 sm:ml-4 grade__form-group">
            <label :for="count" class="grade__form-group font-bold"
              >Credit</label
            >
            <input
              type="number"
              class=" textFont py-2 px-1 sm:px-4 rounded grade__input mb-3"
              v-model="data.unit"
            />
          </div>
          <span
            @click="removePreviousField(index)"
            class="remove-field ml-3 text-white cursor-pointer grade__form-group grade__form-group-2"
            >X</span
          >
        </div>
        <app-button>
          <button
            @click.prevent="addNewField"
            :class="['btn--blue']"
            class=" btn block text-white rounded px-4 py-4 text-xl  font-bold text-center sm:text-2xl font-textFont shadow-xl  mt-6 w-full sm:w-1/2 mx-auto my-6"
          >
            {{ newTitle }}
          </button>
        </app-button>
        <app-button>
          <button
            @click.prevent="calculateGrade"
            :class="['btn--yellow']"
            class=" btn block text-white rounded px-4 py-4 text-xl  font-bold text-center sm:text-2xl font-textFont shadow-xl  mt-6 w-full sm:w-1/2 mx-auto my-6"
          >
            Calculate GPA
          </button>
        </app-button>
        <div class="grade__gpa" v-if="showGPA">
          <p class="text-xl sm:text-2xl">Your GPA is: </p>
          <p>{{ GPA }}</p>
        </div>
      </div>
    </form>
  </section>
</template>

<script>
import Button from '@/components/Button.vue';
export default {
  data() {
    return {
      start: true,
      process: false,
      startTitle: 'Get Started',
      newTitle: 'Add a new field',
      numOfCourses: 5,
      totalUnits: '',
      selected: 'A',
      unit: 0,
      grades:  ['AB', 'B','BC','C', 'CD', 'D', 'E', 'F' ],
      GPA: 0,
      showGPA: false,
      formData: [{ course: '', grade: '', unit: 0 }]
    };
  },
  computed: {
    count() {
      let count = 0;
      return count++;
    }
  },
  components: {
    appButton: Button
  },
  methods: {
    startCalculator() {
      this.start = false;
      this.process = true;
    },
    addNewField() {
      this.formData.push({ course: '', grade: '', unit: '' });
    },
    removePreviousField(index) {
      this.formData.splice(index, 1);
      this.calcul
    },
    calculateGrade() {
      let totalGrades = 0,
        totalUnits = 0,
        GPA = 0;
      const formDataArr = this.formData.map(el => {
        let grade = el.grade;
        let gradePoint = 0;
        let unit = parseInt(el.unit, 10);
        switch (grade) {
          case 'A':
            gradePoint = 4.0 * unit;
            break;
          case 'AB':
            gradePoint = 3.5 * unit;
            break;
          case 'B':
            gradePoint = 3.25 * unit;
            break;
          case 'BC':
            gradePoint = 3.0 * unit;
            break;
          case 'C':
            gradePoint = 2.75 * unit;
            break;
          case 'CD':
            gradePoint = 2.5 * unit;
            break;
          case 'D':
            gradePoint = 2.25 * unit;
            break;
          case 'E':
            gradePoint = 2.0 * unit;
            break;
          case 'F':
            gradePoint = 0 * unit;
            break;
        }
        totalGrades += gradePoint;
        totalUnits += unit;
      });
      console.log(totalGrades, totalUnits);
      GPA = totalGrades / totalUnits;
      this.GPA = GPA;
      this.showGPA = true;
      console.log(formDataArr);
    }
  },
  watch: {}
};
</script>

<style lang="scss" scoped>
.grade {
  width: 100%;
  max-width: 50rem;
  margin: 4rem auto;

  &__input {
    // width: 43%;
    width: 100%;
    border: 3px solid transparent;
    background: var(--color-primary);

    &:focus {
      border: 3px solid var(--color-blue);
      outline: none;
    }

    &-select {
      padding: .7rem;
    }
  }

  &__form-group {
    flex: 1 0 25%;
    &-2 {
      flex: 1 0 6%;
    }
  }

  &__gpa {
    font-size: 3rem;
    background: lightgreen;
    margin-top: 2rem;
    padding: 1rem;
    font-weight: 700;
    text-align: center;
  }
}

.remove-field {
  background: var(--color-paragraph);
  padding: 0.2rem;
}

@media only screen and (min-width: 37.5em) {
  .grade {
    margin: 3rem auto;
  }
}
</style>
