<template>
  <div id="app">
    <invoice-table :data="items" />
  </div>
</template>

<script>
import InvoiceTable from './components/InvoiceTable'

export default {
  name: 'app',
  components: {
    InvoiceTable
  },
  data () {
    return {
      items: []
    }
  }
}
</script>

<style>
#app {
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen,
    Ubuntu, Cantarell, 'Fira Sans', 'Droid Sans', 'Helvetica Neue', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  font-size: 14px;
}

#app * {
  box-sizing: border-box;
}
</style>
