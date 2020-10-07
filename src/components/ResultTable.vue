<template>
  <div id="result-table">
    <!-- <table class="maintable">
      <thead>
        <tr class="maintable__header">
          <th>Date</th>
          <th>Amount to Pay</th>
          <th>Interest</th>
          <th>Base Amount</th>
          <th>Run Balance</th>
        </tr>
      </thead>
      <tbody>
      </tbody>
      
    </table> -->
    <div class="maintable">
      <ul class="maintable__header">
        <li class="maintable--right">Date</li>
        <li>Amount to Pay</li>
        <li>Interest</li>
        <li>Base Amount</li>
        <li>Run Balance</li>
      </ul>
      <TableRow v-for="result in results" :rowData="result" :key="result.date" />
    </div>
  </div>
</template>

<script>
import TableRow from '@/components/TableRow'


export default {
  name: 'ResultTable',
  components: {
    TableRow
  },
  props: {
    results: Array
  }
}
</script>

<style scoped>
#result-table {
  margin-top: 2em;
  width: 100%;
}

.maintable {
  width: 100%;
}

.maintable__header {
  list-style: none;
  display: grid;
  grid-template-columns: repeat(5, 1fr);
  padding-left: 0;
  background: var(--primary-accent);
  border-radius: 15px;
}

.maintable__header li {
  color: #fff;
  padding: 15px 25px;
  /* letter-spacing: 1px; */
  font-weight: 700;
  text-align: end;
}

.maintable--right {
  text-align: left !important;
}

</style>