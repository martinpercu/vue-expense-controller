<script>
import Layout from './Layout.vue'
import Header from './Header.vue'
import Resume from './Resume/Index.vue'
import History from './History/Index.vue'
import Action from './Action.vue'
import Graph from './Resume/Graph.vue'

export default {
  components: {
    Layout,
    Header,
    Resume,
    Action,
    History,
    Graph
  },
  data() {
    return {
      label: null,
      initialAmount: null,
      theExpenses: []
    };
  },
  computed: {
    amounts() {
      const last30DaysExpenses = this.theExpenses
        .filter((e) => {
          const today = new Date();
          const pass30Days = today.setDate(today.getDate() - 30);

          return e.time > pass30Days
        })
        .map((e) => e.amount);
        console.log("last 30 expenses ==> ", last30DaysExpenses);

      return last30DaysExpenses.map((m, i) => {
        const last30Expenses = last30DaysExpenses.slice(0, i+1);
        console.log("each slice  ", last30Expenses);

        return last30Expenses.reduce((addition, expense) => {
          return addition + expense
        }, 0)
      })
    },
    totalAmount() {
      return this.theExpenses.reduce((addition, expense) => {
        return addition + expense.amount
      }, 0)
    }
  },
  mounted() { 
    const theExpensesInLocal = JSON.parse(localStorage.getItem("theExpensesInLocal"));
    if (Array.isArray(theExpensesInLocal)) {
      this.theExpenses = theExpensesInLocal?.map(e => {      
        return { ...e, time: new Date(e.time) }
      });
    }
    
  },
  methods: {
    createExpense(expense) {
      this.theExpenses.push(expense);
      this.updateTheExpenses();
    },
    removeThisFromExpenses(id) {
      const index = this.theExpenses.findIndex((m) => m.id === id);
      this.theExpenses.splice(index, 1);
      this.updateTheExpenses();
    },
    updateTheExpenses() {
      localStorage.setItem("theExpensesInLocal", JSON.stringify(this.theExpenses))
    }
  }
}
</script>

<template>
  <Layout>
    <template #header>
      <Header></Header>
    </template>
    <template #resume>
      <Resume
        :label="'Total Savings'"
        :date-label="dateChoose"
        :total-amount="totalAmount"
        :amount="initialAmount"
      >
        <template #graphic>
          <Graph :amounts="amounts" />
        </template>

        <template #action>
          <Action @sendNewExpense="createExpense"></Action>
        </template>
      </Resume>
    </template>
    <template #history>
      <History :theExpenses="theExpenses" @removeThisExpense="removeThisFromExpenses" />
    </template>
  </Layout>
</template>
