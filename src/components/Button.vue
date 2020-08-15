<template>
  <div>
    <slot></slot>
  </div>
</template>

<script>
export default {
  data() {
    return {};
  },
  props: {
    // title: {
    //   type: String,
    //   required: true
    // },
    color: {
      type: String,
      default: 'blue'
    }
  }
};
</script>

<style lang="scss" scoped>
.btn {
  transition: all 0.2s;
  box-sizing: border-box;


  &:hover {
    transform: scale(1.05);
  }
  &--blue {
    background: var(--color-heading);
    color: var(--color-primary);
  }
  &--yellow {
    background: var(--color-secondary);
    color: var(--color-heading);
  }
}
</style>
