<script setup>
import Layout from './Layout.vue';
import Header from './Header.vue';
import Resume from './Resume/Index.vue';
import History from './History.vue';
</script>

<template>
    <Layout>
        <template #header>
            <Header></Header>
        </template>
        <template #resume>
            <Resume></Resume>
        </template>
        <template #history>
            <History></History>
        </template>
    </Layout>
    
</template>