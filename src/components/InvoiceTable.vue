<template>
  <table>
    <thead>
      <tr>
        <td>Наименование</td>
        <td>Количество</td>
        <td>Цена</td>
        <td>Сумма</td>
        <td></td>
      </tr>
    </thead>

    <tbody>
      <invoice-table-row
        v-for="(row, i) in data"
        :key="i"
        :data="row"
        @save="update(i, $event)"
        @remove="remove(i)"
        />

      <tr
        is="invoice-table-row"
        :data="emptyRow"
        :mode-create="true"
        @save="create($event)"
        />
    </tbody>

    <tfoot>
      <tr>
        <td></td>
        <td colspan="2" class="total">Итог</td>
        <td>{{ total }}</td>
        <td></td>
      </tr>
    </tfoot>
  </table>
</template>

<script>
import InvoiceTableRow from './InvoiceTableRow'

export default {
  name: 'InvoiceTable',

  props: {
    data: {
      type: Array,
      default: () => []
    }
  },

  data () {
    return {
      emptyRow: {
        name: '',
        qty: '',
        price: ''
      }
    }
  },

  components: {
    InvoiceTableRow
  },

  computed: {
    total () {
      return this.data.reduce((result, item) => {
        const qty = parseFloat(item.qty.replace(',', '.'))
        const price = parseFloat(item.price.replace(',', '.'))
        return result + price * qty
      }, 0)
    }
  },

  methods: {
    remove (index) {
      this.data.splice(index, 1)
    },

    update (index, data) {
      this.$set(this.data, index, data)
    },

    create (data) {
      this.data.push(data)
    }
  }
}
</script>

<style scoped>
  table {
    width: 100%;
    border-spacing: 0;
    border-collapse: collapse;
    table-layout: fixed;
  }

  td {
    border: solid 1px #ccc;
    padding: 8px 16px;
  }

  thead td {
    background-color: #eee;
  }

  .total {
    text-align: right;
  }
</style>
