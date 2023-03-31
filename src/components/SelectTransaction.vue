<template>
  <select :id="id" class="">
    <option v-if="transactions.length == 0" value="">
      Đang tải lựa chọn...
    </option>
    <option v-for="trans in transactions" :key="trans.id" :value="trans.id">
      {{ trans.name }}
    </option>
  </select>
</template>

<script>
export default {
  props: {
    id: String,
    transactions: Array,
  },
};
</script>
