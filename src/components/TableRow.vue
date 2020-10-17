<template>
  <div id="table-row">
    <ul class="row">
      <li class="right">{{rowData.date}}</li>
      <li class="right hide type-value">{{rowData.type}}</li>
      <li class="highlight">{{ (rowData.amort)}}</li>
      <li class="hide">{{rowData.interest}}</li>
      <li class="hide">{{rowData.principal}}</li>
      <li class="hide">{{rowData.runBalance}}</li>
    </ul>
    <transition name="show">
      <div class="dropdown-result" v-if="clicked">
        <ul>
          <li>Type</li>
          <li class="type-value">{{rowData.type}}</li>
        </ul>
        <ul>
          <li>Interest</li>
          <li>{{rowData.interest}}</li>
        </ul>
        <ul>
          <li>Principal Amount</li>
          <li>{{rowData.principal}}</li>
        </ul>
        <ul>
          <li>Run Balance</li>
          <li>{{rowData.runBalance}}</li>
        </ul>
      </div>
    </transition>
    <div class="arrow" @click="showMore">
      <img src="../assets/arrow.svg" :class="{clicked : clicked}">
    </div>
  </div>
</template>

<script>
import Accounting from '@/lib/accounting'

export default {
  name: 'TableRow',
  props: {
    rowData: Object
  },
  data () {
    return {
      clicked: false
    }
  },
  methods: {
    showMore() {
      this.clicked = !this.clicked
    }
  }
}
</script>

<style scoped>
#table-row {
  position: relative;
  background: #fff;
  border-radius: 10px;
}

.row {
  position: relative;
  list-style: none;
  display: grid;
  grid-template-columns: repeat(6, 1fr);
  padding-left: 0;
  border-radius: 10px;
  padding-inline-start: 0;
  margin-inline-start: 0;
  margin-inline-end: 0;
  margin-block-end: 0;
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

.arrow {
  position: relative;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: .5em 0;
  display: none;
}

.arrow img {
  /* transform: rotate(180deg); */
  transition: transform .2s ease-in-out;
}

.arrow::before {
  content: '';
  height: 1px;
  width: 75%;
  padding: 0 25px;
  background: #f5f5f5;
  position: absolute;
  top: 0;
}

.dropdown-result {
  display: block;
}

.type-value {
  font-weight: 700;
}

.dropdown-result ul {
  list-style: none;
  display: flex;
  justify-content: space-between;
  padding: 0 25px;
  font-size: 14px;
  color: var(--main-black)
}

.dropdown-result ul li:first-child {
  opacity: 0.7;
}

.clicked {
  transform: rotate(180deg);
  transition: transform .2s ease-in-out;
}

.show-enter-active, .show-leave-active {
  transform: scale(1, 1);
  opacity: 1;
  transition: transform .3s ease-in-out,
              height .3s linear,
              opacity 0.5s ease-in-out;
  transform-origin: top;
  height: 124px;
}
.show-enter, .show-leave-to /* .fade-leave-active below version 2.1.8 */ {
  transform: scale(1, 0);
  transition: height .1s ease-in, opacity 0.1s ease-in-out;
  height: 0;
  opacity: 0;
}


@media screen and (max-width: 767px) {
  .row {
    grid-template-columns: repeat(2, 1fr);
  }

  .row li {
    padding: 15px 25px;
  }

  .arrow {
    display: flex;
  }

}
</style>