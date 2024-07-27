
<script>
export default {
  name: 'Button',
  props: {
    onclick: {
      type: Function,
    },
  },
};
</script>

<template>
  <button @click="onclick">
    <slot></slot>
  </button>
</template>

<style lang="css" scoped>
  button {
    border: 1px solid #06b6d4;
    border-radius: 4px;
    padding: 5px 10px;
    background: none;
    cursor: pointer;
    color: #06b6d4;
    font-size: 16px;
    width: fit-content;
    transition: all 0.1s ease;
  }
  button:hover {
    background: #06b6d4;
    color: white;
  }


</style>
