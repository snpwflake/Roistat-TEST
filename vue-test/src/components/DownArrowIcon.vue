<!-- eslint-disable max-len -->

<script>
export default {
  name: 'DownArrowIcon',
  props: {
    size: {
      type: Number,
      default: 32,
    },
  },
};
</script>
<template>
  <svg xmlns="http://www.w3.org/2000/svg" :width="size" :height="size" viewBox="0 0 24 24" fill="none">
    <path d="M7 10L12 15L17 10" stroke="#000000" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/>
  </svg>
</template>
