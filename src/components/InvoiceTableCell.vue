<template>
  <td :class="[edit ? 'mode-edit' : '']">
     <input v-if="edit" type="text" :value="value" @input="$emit('input', $event.target.value)">
     <span v-else>{{ val }}</span>
  </td>
</template>

<script>
export default {
  name: 'InvoiceTableCell',

  props: {
    val: String,
    value: String,
    edit: false
  }
}
</script>

<style scoped>
  td {
    border: solid 1px #ccc;
    padding: 8px 16px;
  }

  td.mode-edit {
    padding: 0;
    background: moccasin;
  }

  td.mode-edit input {
    width: 100%;
    padding: 8px 16px;
    border: none;
    background: none;
  }
</style>
