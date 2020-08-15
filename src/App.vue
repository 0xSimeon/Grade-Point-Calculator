<template>
  <div id="app">
    <app-grade-point></app-grade-point>
  </div>
</template>

<script>
import GradePoint from '@/components/GradePoint.vue';
export default {
  name: 'App',
  
  components: {
    appGradePoint: GradePoint
  },
};
</script>

<style lang="scss">
// Variables
:root {
  --color-primary: #fffffe;
  --color-secondary: #ffd803;
  --color-tertiary: #bae8e8;
  --color-tertiary-2: #e3f6f5;
  --color-heading: #272343;
  --color-paragraph: #2d334a;
  --color-blue: #7e7edd;
}

*,
*::before,
*::after {
  margin: 0;
  padding: 0;
  box-sizing: inherit;
}

html {
  box-sizing: border-box;
  // font-size: 56.25%;
}

body {
  background: linear-gradient(
    to right,
    var(--color-tertiary),
    var(--color-tertiary-2)
  );
}

h1,
h2,
h3,
h4,
h5,
button {
  color: var(--color-heading);
}

p,
input {
  color: var(--color-paragraph);
}

// @media only screen and (min-width: 37.5em) {
//   html {
//     font-size: 62.5%;
//   }
// }
</style>
