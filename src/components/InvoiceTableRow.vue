<template>
  <tr>
    <invoice-table-cell
      v-for="(val, key) in data"
      :key="key"
      :val="val"
      :edit="edit"
      v-model="model[key]"
      />

    <td>{{ sum }}</td>

    <td v-if="!edit">
      <span class="action" @click="edit = true">редактировать</span>
      <span class="action" @click="$emit('remove')">удалить</span>
    </td>

    <td v-if="edit">
      <span class="action" @click="save">сохранить</span>
      <span v-if="!modeCreate" class="action" @click="edit = false">отмена</span>
    </td>
  </tr>
</template>

<script>
import Vue from 'vue'
import InvoiceTableCell from './InvoiceTableCell'

export default {
  name: 'InvoiceTableRow',

  components: {
    InvoiceTableCell
  },

  props: {
    data: Object,
    modeCreate: {
      type: Boolean,
      default: false
    }
  },

  data () {
    return {
      model: Vue.util.extend({}, this.data),
      edit: this.modeCreate
    }
  },

  computed: {
    sum () {
      return this.data.qty * this.data.price
    }
  },

  methods: {
    save () {
      const copy = Vue.util.extend({}, this.model)
      this.$emit('save', copy)

      if (this.modeCreate) {
        this.clearModel()
      } else {
        this.edit = false
      }
    },

    clearModel () {
      Object.keys(this.model).forEach(prop => {
        this.model[prop] = ''
      })
    }
  }
}
</script>

<style scoped>
  td {
    border: solid 1px #ccc;
    padding: 8px 16px;
  }

  .action {
    color: tomato;
    cursor: pointer;
    font-variant: small-caps;
  }

  .action:not(:last-child):after {
    content: ' | '
  }
</style>
