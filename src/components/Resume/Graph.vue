<script setup>
import { toRefs , computed } from 'vue';


const props = defineProps({
    amounts: {
        type: Array,
        default: () => [],
    }
});

const { amounts } = toRefs(props);

const amountToPixels = () => {
    const min = Math.min(...amounts.value);
    const max = Math.max(...amounts.value);
    return `${min},${max}`
};


const points = computed(() => {
    const total = amounts.value.length;
    return Array(total).fill(110).reduce((points, amount, i) => {
        const x = (300 / total) * (i + 1);
        const y = amountToPixels(amount);
        return `${points} ${x},${y}`;
    }, "0, 100");
})



</script>

<template>
    <div>
        <svg viewBox="0 0 330 220">
            <line 
                stroke="#c0c0c0" 
                stroke-width="3"
                x1="0"
                y1="110"
                x2="330"
                y2="110"
            />
            <polyline
                fill="none"
                stroke="#0689c0"
                stroke-width="3"
                :points="points"
            />
            <line 
                stroke="green" 
                stroke-width="3"
                x1="180"
                y1="0"
                x2="180"
                y2="220"/>
        </svg>
        <p>Last 30 days</p>
    </div>
</template>



<style scoped>
svg {
  width: 100%;
}
p {
  text-align: center;
}
</style>