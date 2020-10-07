<template>
  <div class="home">
    <AmortForm />
    <!-- <ResultTable /> -->
  </div>
</template>

<script>
// @ is an alias to /src
import AmortForm from '@/components/AmortForm'
// import ResultTable from '@/components/ResultTable'

export default {
  name: 'Home',
  components: {
    AmortForm,
    // ResultTable
  }
}
</script>

<style scoped>
.home {
  flex-direction: column;
}
</style>