<template>
  <div id="amort-form">
    <form class="mainform">
      <h2 class="mainform__title">Payment Details</h2>
      <div class="mainform__body">
        <div class="mainform__amount">
          <label for="totalamount"><h3>Total Amount</h3></label>
          <input type="text" class="totalamount" id="totalamount">
        </div>
        <div class="mainform__downpayment">
          <h3>Downpayment</h3>
          <div class="mini-inputs">
            <div>
              <label>%</label>
              <input type="text" class="totalamount" id="totalamount">
            </div>
            <div>
              <label>Interest Rate</label>
              <input type="text" class="totalamount" id="totalamount" placeholder="%">
            </div>
            <div>
              <label>Term/s</label>
              <input type="text" class="totalamount" id="totalamount">
            </div>
          </div>
        </div>

        <div class="mainform__amortization">
          <h3>Amortization</h3>
          <div class="mini-inputs">
            <div>
              <label>%</label>
              <input type="text" class="totalamount" id="totalamount">
            </div>
            <div>
              <label>Interest Rate</label>
              <input type="text" class="totalamount" id="totalamount" placeholder="%">
            </div>
            <div>
              <label>Term/s</label>
              <input type="text" class="totalamount" id="totalamount">
            </div>
          </div>
        </div>
      </div>
      <div class="mainform__button">
        <button> Calculate </button>
      </div>
    </form>
  </div>
</template>

<script>
export default {
  name: 'AmortForm',

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

.mainform__amount {
  grid-column: 1 / 3;
  display: flex;
  flex-direction: column;
  width: 400px;
}

.mainform__amount h3 {
  margin: 0;
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