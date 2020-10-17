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
        <li class="maintable--right hide">Type</li>
        <li>Amount to Pay</li>
        <li class="hide">Interest</li>
        <li class="hide">Base Amount</li>
        <li class="hide">Run Balance</li>
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
  data () {
    return {
      headerOffset: null
    }
  },
  props: {
    results: Array
  },
  methods: {
    onScroll() {
      const theheader = document.querySelector('.maintable__header')
      let mainWidth = document.querySelector('#table-row').clientWidth

      if (this.headerOffset <= document.scrollingElement.scrollTop) {
        theheader.classList.add('stickey')
        theheader.style.width = `${mainWidth}px`
      } else {
        theheader.classList.remove('stickey')
      }
    }
  },
  created() {
    window.addEventListener('scroll', this.onScroll, false)
  },
  mounted() {
    this.headerOffset = document.querySelector('.maintable__header').offsetTop
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
  grid-template-columns: repeat(6, 1fr);
  padding-left: 0;
  background: var(--primary-accent);
  border-radius: 15px;
  z-index: 3;
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

.stickey {
  position: fixed;
  top: 0;
}

@media screen and (max-width: 767px) {
  .maintable__header {
  grid-template-columns: repeat(2, 1fr);

  }
}
</style>