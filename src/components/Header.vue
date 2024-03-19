<script>
export default {
    methods: {
        reload() {
            location.reload();
        }
    },
};
</script>

<template>
    <header>
        <font-awesome-icon 
        @click="reload"
        class="filterDollarHeader" 
        :icon="['fas', 'filter-circle-dollar']" 
        />
        <h1>Cash<span>Expenses</span></h1>
        <span></span>        
    </header>
</template>


<style scoped>
header {
    display: flex;
    justify-content: space-around;
    align-items: center;
    width: 100vw;
}

h1 {
    color: var(--brand-blue);
}

h1 span {
    color: var(--brand-green);
}


.filterDollarHeader {
    height: 6vh;
    color: var(--brand-green);
}

</style>