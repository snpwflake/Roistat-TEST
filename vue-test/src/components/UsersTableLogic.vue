<script>
import Table from '@/components/Table.vue';
import ModalAddUser from '@/components/ModalAddUser.vue';

const columns = [
  {
    id: 'id',
    name: 'Индекс',
    align: 'center',
  },
  {
    id: 'name',
    name: 'Имя',
    align: 'center',
  },
  {
    id: 'phone',
    name: 'Телефон',
    align: 'center',
  },
];
function addChildArrayByIdRecursive(arr, targetId, newChildrenArray) {
  // Рекурсивно ищем объект в массиве
  // eslint-disable-next-line no-restricted-syntax
  for (const obj of arr) {
    if (obj.id === targetId) {
      // Добавляем новый массив объектов в ключ children
      obj.children = [...obj.children, ...newChildrenArray];
      return true; // Возвращаем true, если нашли и изменили объект
    }
    if (obj.children) {
      const found = addChildArrayByIdRecursive(obj.children, targetId, newChildrenArray);
      if (found) {
        return true; // Возвращаем true, если нашли и изменили объект
      }
    }
  }
  return false; // Возвращаем false, если не нашли и не изменили объект
}

export default {
  name: 'UsersTableLogic',
  components: {
    Table,
    ModalAddUser,
  },
  data() {
    return {
      columns,
      tableData: [],
    };
  },
  methods: {
    addUser(user) {
      if (!user.chief) {
        this.tableData.push(user);
        this.tableData = [...this.tableData];
      } else {
        const users = this.tableData;
        addChildArrayByIdRecursive(users, user.chief, [user]);
        this.tableData = [...users];
      }
    },
  },
  mounted() {
    this.tableData = JSON.parse(localStorage.getItem('users')) || [];
  },
  watch: {
    tableData() {
      localStorage.setItem('users', JSON.stringify(this.tableData));
    },
  },
};
</script>

<template>
   <div :class="'users__container'">
    <Table @addUser="addUser" :tableData="tableData" :columns="columns" />
   </div>
</template>

<style lang="css">
.users__container {
  padding: 20px;
  display: flex;
  flex-direction: column;
  gap: 20px;
}
</style>
