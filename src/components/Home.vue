<script setup>
import Layout from './Layout.vue';
import Header from './Header.vue';
import Resume from './Resume/Index.vue';
import History from './History/Index.vue';
import Action from './Action.vue';
import Graph from './Resume/Graph.vue';

const initialAmount = null;
// const initialAmount = 548700;
const dateChoose = "15/15/2015";

const amounts = [40, 220, 150, -48, -150, 450, 40];
// const amounts = [40, 220, 150, -48, -150, 20];
// const amounts = [10, -5, 12, -20];
// const amounts = [10, 0, 12, -20, 15, 20];
// const amounts = [10, -20];




const theExpenses = [{
    id: 0,
    title: "expense N°1",
    description: "loren etc etc qsdflikje bla bla",
    amount: 525
    },
    {
    id: 1,
    title: "expense N°2",
    description: "loren etc etc qsdflikje bla bla",
    amount: -252
    },
    {
    id: 2,
    title: "expense N°3",
    description: "loren etc etc qsdflikje bla bla",
    amount: 227
    },
    {
    id: 3,
    title: "expense N°4",
    description: "loren etc etc qsdflikje bla bla",
    amount: 156
    },
]

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