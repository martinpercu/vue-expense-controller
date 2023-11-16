<script setup>
import { toRefs , computed } from 'vue';


const props = defineProps({
    amounts: {
        type: Array,
        default: () => [],
    }
});

const { amounts } = toRefs(props);

const amountToPixels = (amount) => {
    const min = Math.min(...amounts.value);
    const max = Math.max(...amounts.value);

    const amountAbsolute = amount + Math.abs(min);
    const minPlusMax = Math.abs(max) + Math.abs(min);

    // 110 is the totalHalf heigh ===> the "y" 
    // We need to invert the values using "totalHeigh" minus "the logic" because coordenates in html are inverted.

    const theReturn = 220 - ((amountAbsolute * 110) / minPlusMax) * 2;

    return theReturn
};


const points = computed(() => {
    const total = amounts.value.length;
    return amounts.value.reduce((points, amount, i) => {
        // 330 is the total pixel width
        const x = (330 / total) * (i + 1);
        const y = amountToPixels(amount);
        console.log(y);
        return `${points} ${x},${y}`;
    },"0, 100");
});

// to draw the zero value line wi get create a const yZeroLine
const yZeroLine = computed(() => {
    return amountToPixels(0)
});



</script>

<template>
    <div>
        <svg viewBox="0 0 330 220">
            <line 
                stroke="#c0c0c0" 
                stroke-width="3"
                x1="0"
                :y1="yZeroLine"
                x2="330"
                :y2="yZeroLine"
            />
            <polyline
                fill="none"
                stroke="#0689c0"
                stroke-width="3"
                :points="points"
            />
            <line 
                stroke="green" 
                stroke-width="2"
                x1="240"
                y1="0"
                x2="240"
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