<template>
  <the-header :totalIncome="state.totalIncome" />
  <the-form :state="state" @add-income="AddIncome" />
  <IncomeList :state="state" @remove-item="removeItem" />
</template>

<script>
import { reactive, computed } from 'vue';
import TheHeader from './components/TheHeader';
import TheForm from './components/TheForm';
import IncomeList from './components/IncomeList';
export default {
  components: {TheForm, TheHeader},
  setup () {
    const state = reactive({
      income: [],
      sortedIncome: computed(() => {
        let temp = [];

        // eslint-disable-next-line vue/no-side-effects-in-computed-properties
        temp = state.income.sort(function (a, b) {
          return b.date - a.date;
        });
        return temp;
      }),
      totalIncome: computed(() => {
        let temp = 0;
        if (state.income.length > 0) {
          for (let i = 0; i < state.income.length; i++) {
            temp += state.income[i].value;
          }
          return temp;
        } else {
          return 0;
        }
      })
    });
    function AddIncome(obj) {
      let d = obj.date.split("-");
      let newD = new Date(d[0], d[1], d[2]);
      state.income = [...state.income, {
        id: Date.now(),
        desc: obj.desc,
        value: parseInt(obj.value),
        date: newD.getTime()
      }]
    }
    function removeItem(id) {
      state.income = state.income.filter(v => v.id != id);
    }
    // Return template data
    return {
      TheHeader,
      IncomeList,
      TheForm,
      state,
      AddIncome,
      removeItem
    }
  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Fira Sans', sans-serif;
}
body {
  background: #EEE;
}
</style>
