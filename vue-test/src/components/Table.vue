<script>
import ModalAddUser from '@/components/ModalAddUser.vue';


export default {
  components: { ModalAddUser },
  name: 'Table',
  props: {
    columns: {
      type: Array,
      required: true,
    },
    firstTable: {
      type: Boolean,
      default: true,
    },
    defaultChief: {
      type: Object,
      default: null,
    },
    tableData: {
      type: Array,
      default: () => [],
    },
  },
  methods: {
    addUser(user) {
      this.$emit('addUser', user);
    },
  },
};
</script>

<template>
  <div class="table__container">
    <ModalAddUser @addUser="addUser" :options="tableData" :defaultChief="defaultChief"/>
    <table>
      <thead>
        <tr>
          <th align="center" width="32px"></th>
          <th v-for="column in columns"
            :key="column.id"
            :align="column.align">
            {{ column.name }}
          </th>
        </tr>
      </thead>
        <template v-for="row in tableData">
          <tr :key="row.id">
            <td align="center">
              <button v-if="row.children" @click="row.isExpanded = !row.isExpanded">+</button>
            </td>
            <td v-for="column in columns"
              :key="column.id"
              :align="column.align">
              {{ row[column.id] }}
            </td>
          </tr>
          <td
            :colspan="row.children ? columns.length + 1 : columns.length"
            v-if="row.children && row.isExpanded"
            :key="row.id"
          >
            <div class="children__container">
              <Table
                @addUser="addUser"
                :firstTable="false"
                :tableData="row.children"
                :columns="columns"
                :defaultChief="{id: row.id, name: row.name}"
              />
            </div>
          </td>
        </template>
    </table>
  </div>
</template>


<style lang="css" scoped>
  .table__container {
    overflow: auto;
  }
  .children__container {
    padding-top: 16px;
    display: flex;
    border: 1px solid #06b6d4;
    border-top: 0;
    flex-direction: column;
    gap: 12px;
  }
  table {
    width: 100%;
  }

  table, th, td {
    padding: 10px 0;
    border: 1px solid black;
    border-collapse: collapse;
  }

  tr:hover > td {
    background: #f5f5f5;
    transition: all 0.1s ease;
  }

  tr > th {
    background: #06b6d4;
    color: white;
  }
</style>

