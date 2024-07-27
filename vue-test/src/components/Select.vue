<script>
export default {
  name: 'Select',
  props: {
    options: {
      type: Array,
      required: true,
    },
    selectedOption: {
      type: Object,
      default: null,
    },
    placeholder: {
      type: String,
      default: 'Выберите значение',
    },
  },
  data() {
    return {
      areOptionsVisible: false,
    };
  },
  methods: {
    selectOption(option) {
      this.areOptionsVisible = false;
      this.$emit('select', option);
    },
    hideOptions() {
      this.areOptionsVisible = false;
    },
  },

  mounted() {
    document.addEventListener('click', this.hideOptions, true);
  },

  beforeDestroy() {
    document.removeEventListener('click', this.hideOptions, true);
  },
};
</script>

<template>
  <div class="select">
    <p @click="areOptionsVisible = !areOptionsVisible"
      class="selected__option">
      {{ selectedOption != null ? selectedOption.name : placeholder }}
    </p>
    <div
      v-show="areOptionsVisible"
      class="select__options"
    >
      <p v-if="options.length === 0">Нет данных</p>
      <p v-for="option in options"
      @click="selectOption(option)"
        class="select__option"
        :key="option.id"
      >
        {{ option.name }}
      </p>
    </div>
  </div>
</template>

<style lang="css">
.select {
  position: relative;
}
.selected__option {
  margin: 0;
  padding: 5px 10px;
  border: 1px solid #ccc;
  cursor: pointer;
}
.select__options {
  z-index: 10;
  position: absolute;
  left: 0;
  margin-top: 4px;
  right: 0;
  border: 1px solid #ccc;
  background: #fff;
  z-index: 1;
}
.select__option {
  margin: 0;
  padding: 8px 10px;
  cursor: pointer;
}

.selected-active {
  background: #ccc;
}
</style>
