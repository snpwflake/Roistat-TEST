<script>
import Button from '@/components/Button.vue';
import Modal from '@/components/Modal.vue';
import SelectChief from './SelectChief.vue';


export default {
  name: 'ModalAdduser',
  components: {
    Button,
    Modal,
    SelectChief,
  },
  props: {
    options: {
      type: Array,
      default: () => [],
    },
    defaultChief: {
      type: Object,
      default: null,
    },
  },
  data() {
    return {
      isModalVisible: false,
      name: '',
      phone: '',
      selectedOption: this.defaultChief,
    };
  },
  methods: {
    showModal() {
      this.isModalVisible = true;
    },
    closeModal() {
      this.isModalVisible = false;
    },
    onOk() {
      this.isModalVisible = false;
      const newUser = {
        id: +new Date(),
        name: this.name,
        phone: this.phone,
        children: [],
        isExpanded: false,
        chief: this.selectedOption !== null ? this.selectedOption.id : null,
      };
      this.$emit('addUser', newUser);
    },
    changeName(e) {
      this.name = e.target.value;
    },
    changePhone(e) {
      this.phone = e.target.value;
    },
    changeSelectedOption(option) {
      this.selectedOption = option;
    },
  },
};

</script>

<template>
  <div class="add-user">
    <Button :onclick="showModal">Добавить пользователя</Button>
    <Modal
      v-show="isModalVisible"
      @close="closeModal"
      @ok="onOk"
      :buttonOk="'Добавить'"
      :buttonCancel="'Отмена'"
      :title="'Добавить пользователя'"
    >
      <input @change="changeName" placeholder="Имя" class="modal__input" type="text" name="">
      <input @change="changePhone" placeholder="Телефон" class="modal__input" type="tel" name="">
      <SelectChief @select="changeSelectedOption" :options="options" />
    </Modal>
  </div>
</template>

<style >
  .modal__input {
    border: 1px solid #ccc;
    border-radius: 4px;
    padding: 5px 10px;
    background: none;
    cursor: pointer;
    font-size: 16px;
    transition: all 0.1s ease;
    margin-bottom: 16px;
  }
  .modal__input:focus {
    outline: none;
    border: 1px solid #06b6d4;
  }
</style>
