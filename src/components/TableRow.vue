<template>
  <div id="table-row">
    <ul class="row">
      <li class="right">{{rowData.date}}</li>
      <li class="highlight">{{ (rowData.amort)}}</li>
      <li>{{rowData.interest}}</li>
      <li>{{rowData.principal}}</li>
      <li>{{rowData.runBalance}}</li>
    </ul>
  </div>
</template>

<script>
import Accounting from '@/lib/accounting'

export default {
  name: 'TableRow',
  props: {
    rowData: Object
  }
}
</script>

<style scoped>
#table-row {
  background: #fff;
  border-radius: 10px;
}

.row {
  list-style: none;
  display: grid;
  grid-template-columns: repeat(5, 1fr);
  padding-left: 0;
  border-radius: 10px;
}

.row li {
  padding: 25px;
  text-align: end;
  font-size: 15px;
  color: var(--main-black);
}


.right {
  text-align: left !important;
}

.highlight {
  font-weight: 700;
  color: var(--primary-accent) !important;
}

</style>