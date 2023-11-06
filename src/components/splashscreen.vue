<template>
    <div class="splashscreen">
        <font-awesome-icon class="filterDollar" :icon="['fas', 'filter-circle-dollar']" />
        <h1>Cash<span>Expenses</span></h1>
    </div>
</template>

<style scoped>

.splashscreen {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    height: 100vh;
}

h1 {
    color: var(--brand-blue);
}

h1 span {
    color: var(--brand-green);
}

.filterDollar {
    height: 16vh;
    color: var(--brand-green);
}

</style>