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
      theExpenses: [
        {
          id: 0,
          title: 'expense N°1',
          description: 'loren etc etc qsdflikje bla bla',
          amount: 120,
          time: new Date('10-25-2023')
        },
        {
          id: 1,
          title: 'expense N°2',
          description: 'loren etc etc qsdflikje bla bla',
          amount: -75,
          time: new Date('11-14-2023')
        },
        {
          id: 2,
          title: 'expense N°3',
          description: 'loren etc etc qsdflikje bla bla',
          amount: -50,
          time: new Date('09-14-2023')
        },
        {
          id: 3,
          title: 'expense N°4',
          description: 'loren etc etc qsdflikje bla bla',
          amount: 55,
          time: new Date('11-14-2023')
        },
        {
          id: 4,
          title: 'expense N°5',
          description: 'loren etc etc qsdflikje bla bla',
          amount: -80,
          time: new Date('11-14-2023')
        }
      ]
    }
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
    }
  },
  methods: {
    createExpense(movement) {
      this.theExpenses.push(movement)
    },
    removeThisFromExpenses(id) {
      const index = this.theExpenses.findIndex((m) => m.id === id)
      this.theExpenses.splice(index, 1)
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
        :total-amount="850000"
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
