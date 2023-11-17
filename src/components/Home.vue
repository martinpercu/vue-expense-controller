<script setup>
import Layout from './Layout.vue';
import Header from './Header.vue';
import Resume from './Resume/Index.vue';
import History from './History/Index.vue';
import Action from './Action.vue';
import Graph from './Resume/Graph.vue';

import { computed } from 'vue';

const initialAmount = null;
// const initialAmount = 548700;
const dateChoose = "15/15/2015";

// const amounts = [40, 220, 150, -48, -150, 450, 40];
// const amounts = [40, 220, 150, -48, -150, 20];
// const amounts = [10, -5, 12, -20];
// const amounts = [10, 0, 12, -20, 15, 20];
// const amounts = [10, -20];
// const amounts = [1, -1, 1, 0];
// const amounts = [1, -1, 1, 0, 0, 1, 0];
// const amounts = [0, -1, 1, 0, 0.5];
// const amounts = [120, -10, -50, 25, -80];

const theExpenses = [{
    id: 0,
    title: "expense N°1",
    description: "loren etc etc qsdflikje bla bla",
    amount: 120,
    time: new Date("10-25-2023")
    },
    {
    id: 1,
    title: "expense N°2",
    description: "loren etc etc qsdflikje bla bla",
    amount: -75,
    time: new Date("11-14-2023")
    },
    {
    id: 2,
    title: "expense N°3",
    description: "loren etc etc qsdflikje bla bla",
    amount: -50,
    time: new Date("09-14-2023")
    },
    {
    id: 3,
    title: "expense N°4",
    description: "loren etc etc qsdflikje bla bla",
    amount: 55,
    time: new Date("11-14-2023")
    },
    {
    id: 4,
    title: "expense N°5",
    description: "loren etc etc qsdflikje bla bla",
    amount: -80,
    time: new Date("11-14-2023")
    }
];

// const amounts = theExpenses.map(({amount}) => amount);

const amounts = computed(() => {
    const last30DaysExpenses = theExpenses
        .filter(e => {
            const today = new Date();
            const pass30Days = today.setDate(today.getDate() - 30);
            return e.time >= pass30Days;
        })
        .map(({amount}) => amount);
        console.log("last 30 expenses ==> ", last30DaysExpenses);

    return last30DaysExpenses.map((m, i) => {
        const last30Expenses = last30DaysExpenses.slice(0, i+1);
        console.log("each slice  ", last30Expenses);

        return last30Expenses.reduce((addition, expense) => {
            return addition + expense
        }, 0);
    })
});

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
                    <Action></Action>
                </template>
        
            </Resume>
        </template>
        <template #history>
            <History :expenses="theExpenses">
            </History>
        </template>
    </Layout>
    
</template>