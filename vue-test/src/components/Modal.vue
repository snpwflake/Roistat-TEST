<script>
import Icon from './CloseIcon.vue';

export default {
  name: 'Modal',
  components: {
    Icon,
  },
  props: {
    title: {
      type: String,
      required: true,
    },

    buttonOk: {
      type: String,
      default: 'OK',
    },

    buttonCancel: {
      type: String,
      default: 'Cancel',
    },

    open: {
      type: Boolean,
      default: false,
    },
  },
  setup() {
    return {
      open,
    };
  },

  methods: {
    close() {
      this.$emit('close');
    },

    closeModalFromBackground(e) {
      if (e.target.classList.contains('modal__background')) {
        this.$emit('close');
      }
    },
  },
};
</script>

<template>
  <div>
    <div @click="closeModalFromBackground" class="modal__background">
      <div class="modal__container">
        <header>
          <h2>{{ title }}</h2>
          <button @click="close"><Icon iconName="close"/></button>
        </header>

        <main class="modal__content">
          <slot></slot>
        </main>

        <footer>
          <button @click="$emit('ok')">{{ buttonOk }}</button>
          <button @click="close">{{ buttonCancel }}</button>
        </footer>
      </div>
    </div>
  </div>

</template>

<style>
  header h2 {
    margin: 0;
    font-weight: normal;
    font-size: 18px;
  }
  header button {
    border: none;
    background: none;
    cursor: pointer;
    margin: 0;
    padding: 0;
    transition: all 0.1s ease;
  }
  header button:active {
    scale: 0.9;
  }
  .modal__background {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: rgba(0, 0, 0, 0.5);
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .modal__container {
    max-width: 500px;
    margin: 0 16px;
    padding: 16px;
    background: white;
  }

  header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    color: #06b6d4;
    font-size: 18px;
    font-weight: bold;
    margin-bottom: 16px;
    gap: 10px;
  }

  footer {
    display: flex;
    justify-content: flex-end;
    margin-top: 16px;
    gap: 10px;
  }
  footer button {
    padding: 5px 10px;
    border: 1px solid #06b6d4;
    border-radius: 4px;
    background: #06b6d4;
    color: white;
    cursor: pointer;
    transition: all 0.1s ease;
  }

  footer button:hover {
    background: none;
    color: #06b6d4;
  }

  .modal__content {
    display: flex;
    flex-direction: column;
    padding: 0;
    margin-bottom: 16px;
  }
</style>
