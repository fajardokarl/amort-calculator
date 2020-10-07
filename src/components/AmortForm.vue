<template>
  <div id="amort-form">
    <form class="mainform" @submit.prevent="calculateAmort">
      <h2 class="mainform__title">Payment Details</h2>
      <div class="mainform__body">
        <div class="mainform__amount">
          <label for="totalamount"><h3>Total Amount</h3></label>
          <input
            type="number"
            class="totalamount"
            v-model="totalAmount"
            required
          />
        </div>
        <div class="mainform__date">
          <label><h3>Start Date</h3></label>
          <input
            type="date"
            v-model="startDate"
            required
          />
        </div>
        <div class="mainform__downpayment">
          <h3>Downpayment</h3>
          <div class="mini-inputs">
            <div>
              <label>%</label>
              <input
                type="number"
                v-model="dpPercentage"
                max="100"
              />
            </div>
            <div>
              <label>Interest Rate</label>
              <input
                type="number"
                v-model="dpInterestRate"
              />
            </div>
            <div>
              <label>Term/s</label>
              <input
                type="number"
                v-model="dpTerms"
              />
            </div>
          </div>
        </div>

        <div class="mainform__amortization">
          <h3>Amortization</h3>
          <div class="mini-inputs">
            <div>
              <label>%</label>
              <input
                type="number"
                v-model="balPercentage"
                readonly
              />
            </div>
            <div>
              <label>Interest Rate</label>
              <input
                type="text"
                v-model="balInterestRate"
              />
            </div>
            <div>
              <label>Term/s</label>
              <input
                type="text"
                v-model="balTerms"
              />
            </div>
          </div>
        </div>
      </div>
      <div class="mainform__button">
        <button> Calculate </button>
      </div>
    </form>

    <!-- <div>
      <div v-for="result in results" :key="result.currentDate">
        {{ result }}
      </div>
    </div> -->
    <ResultTable :results=results />

  </div>
</template>

<script>
import Accounting from '@/lib/accounting'
import moment from 'moment'
import ResultTable from '@/components/ResultTable'

export default {
  name: 'AmortForm',
  components: {
    ResultTable
  },
  watch: {
    dpPercentage (val) {
      this.balPercentage = val && val <= 100 ? 100 - val : ''
    }
  },
  data () {
    return {
      totalAmount: '',
      startDate: new Date().toISOString().substr(0, 10),
      dpPercentage: '',
      dpInterestRate: '',
      dpTerms: '',  
      balPercentage: '',
      balInterestRate: '',
      balTerms: '',
      runBalance: '',
      results: []
    }
  },
  methods: {
    calculateAmort () {
      this.results = []
      this.runBalance = this.totalAmount
      Promise.resolve()
      .then(
        this.calculateAll(this.totalAmount, this.dpPercentage, this.dpInterestRate, this.dpTerms)
      ).then(
        this.calculateAll(this.totalAmount, this.balPercentage, this.balInterestRate, this.balTerms)
      )
      console.log(this.results)

    },
    calculateAll (totalAmount, percentage, interestRate, terms) {
      
      const newTotalAmount = totalAmount * (percentage / 100)
      const interest = (interestRate / 100) / 12;
      const monthlyWithInterest = ((newTotalAmount * (Math.pow((1 + interest), terms)) * interest) / (Math.pow((1 + interest), terms) - 1));
      
      let totalprincipal = 0
      let dpRunBal = newTotalAmount
      let currentDate  = moment(this.startDate).format('MMM DD, YYYY')


      for (let i = 0; i < terms; i++) {
        currentDate = moment(this.startDate).add(1, 'month').format('MMM DD, YYYY')
        this.startDate = currentDate

        if (interestRate > 0) {
          // calculate monthly principal with interest

          const interestAmount = dpRunBal * interest
          const principal = monthlyWithInterest - interestAmount


          this.runBalance -= principal
          dpRunBal -= principal
          // totalprincipal += parseFloat(principal.toPrecision(2))

          const tempRunBal = Math.round(Accounting.toFixed(this.runBalance, 2) * 10) / 10

          // console.log(`${monthlyWithInterest} - ${interestAmount} ===> ${principal.toPrecision(2)}`)
          // console.log(currentDate)
          console.log('Run Bal', i, this.runBalance)
          
          this.results = [
            ...this.results, {
              'date': currentDate, 
              'amort': Accounting.formatMoney(monthlyWithInterest, ''),
              'interest': Accounting.formatMoney(interestAmount, ''),
              'principal': Accounting.formatMoney(principal, ''),
              'runBalance': Accounting.formatMoney(tempRunBal, '')
            }
          ]

        } else {
          // calculate monthly
          const monthly = newTotalAmount / terms
          const interest = 0

          this.runBalance -= Accounting.toFixed(monthly, 2)
          const tempRunBal = Math.round(Accounting.toFixed(this.runBalance, 2) * 10) / 10
          // console.log(i, this.runBalance)
          console.log(monthly,  monthly.toPrecision(2))
          
          this.results = [
            ...this.results, {
              'date': currentDate, 
              'amort': monthly,
              'interest': interestAmount,
              'principal': monthly,
              'runBalance': tempRunBal
            }
          ]
        }
      }
    }
  }
}
</script>

<style>

#amort-form {
  width: 100%;

}
.mainform {
  margin-top: 10px;
  background: #fff;
  border-radius: 15px;
  position: relative;
}

.totalamount {
  padding: 12.5px 8px;
  text-align: right;
}

.mainform__title {
  margin: 0 auto;
  padding: 10px 0;
  color: #fff;
  width: 100%;
  border-radius: 15px 15px 0 0;
  text-align: center;
  background: var(--primary-accent);
}
.mainform__body {
  margin: 1em 5em;
  display: grid;
  grid-template: 1fr 1fr / 1fr 1fr;
  column-gap: 5em;
}

.mainform__body h3 {
  margin: 20px 8px;
  color: var(--main-black)
}

.mainform__downpayment, .mainform__amortization {
  position: relative;
}

.mainform__button {
  margin: 1em 5em;
  padding: 2em 0;
  display: flex;
  justify-content: flex-end;
}

.mainform__button button {
  cursor: pointer;
  color: #fff;
  background: var(--yellow-accent);
  border: none;
  border-radius: 25px;
  padding: 10px 25px;
  text-align: center; 
  font-size: 25px;
  font-weight: 600;
}

.mainform__amount, .mainform__date {
  /* grid-column: 1 / 3; */
  display: flex;
  flex-direction: column;
  width: 400px;
}

.mainform__amount h3, .mainform__date h3 {
  margin: 1em 0px;
}

.mini-inputs {
  display: grid;
  justify-content: space-between;
  grid-template-columns: 1fr 1fr 1fr;
  grid-column-gap: 1em;
}

.mini-inputs div {
    width: 100%;
    display: flex;
    flex-direction: column;
    justify-content: flex-end;
}

@media (max-width: 800px) {
  .mainform__body {
    grid-template: 1fr / 1fr;
  }

  .mainform__amount {
    grid-column: 1 / 2;
  }
}

</style>