<script>
import Select from '@/components/Select.vue';

export default {
  name: 'SelectChief',
  components: {
    Select,
  },
  props: {
    options: {
      type: Array,
      default: () => [],
    },
  },
  data() {
    return {
      placeholder: 'Выберите значение',
      selectedOption: null,
      oldOptions: this.options,
    };
  },
  methods: {
    selectOption(option) {
      this.selectedOption = option;

      this.$emit('select', option);
    },
  },
};
</script>


<template>
  <Select
    :options="options"
    :placeholder="placeholder"
    :selectedOption="selectedOption"
    @select="selectOption"
  />
</template>
