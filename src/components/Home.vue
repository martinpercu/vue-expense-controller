<script setup>
import Layout from './Layout.vue';
import Header from './Header.vue';
import Resume from './Resume/Index.vue';
import History from './History.vue';

const initialAmount = null;
// const initialAmount = 548700;
const dateChoose = "15/15/2015";

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
                    <div>
                        GraPHIC
                    </div>
                </template>

                <template #action>
                    <div>
                        Action button
                    </div>
                </template>
        
            </Resume>
        </template>
        <template #history>
            <History></History>
        </template>
    </Layout>
    
</template>