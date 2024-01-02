<template>
  <div>
    <table>
      <thead>
      <tr>
        <th>Лекарственный препарат</th>
        <th>Путь приема</th>
        <th>Дозировка</th>
        <th>Начало приёма</th>
        <th>Конец приёма</th>
        <th>Номер сеанса</th>
        <th>Дней</th>
        <th></th>
      </tr>
      </thead>
      <tbody>
      <tr v-for="item in data" :key="item.number">
        <td>{{ item.name }}</td>
        <td>{{ item.reception }}</td>
        <td>{{ item.dosage }}</td>
        <td>{{ item.start }}</td>
        <td>{{ item.end }}</td>
        <td>{{ item.number }}</td>
        <td>{{ item.days }}</td>
        <td>
          <span class="material-icons" @click="deleteRow(item.number)">delete</span>
        </td>
      </tr>
      </tbody>
    </table>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import type { PropType } from 'vue';

export default defineComponent({
  props: {
    data: {
      type: Array as PropType<Array<{
        name: string; reception: string;
        dosage: string; start: string; end: string;
        number: number; days: number; }>>,
      required: true,
    },
  },
  methods: {
    deleteRow(number: number) {
      this.$emit('delete-row', number);
    },
  },
});
</script>


<style scoped>
table {
  border-collapse: collapse;
  width: 80%;
}

th, td {
  border: 1px solid #ddd;
  padding: 5px;
  text-align: center;
}
</style>

