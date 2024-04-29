<script setup>
import { toRefs , computed, ref, watch } from 'vue';


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
    const total = amounts.value.length - 1;
    return amounts.value.reduce((points, amount, i) => {
        // 330 is the total pixel width
        const x = (330 / total) * i;
        console.log(total, i);
        const y = amountToPixels(amount);
        console.log("x , y  ==> ", x, y);
        return `${points} ${x},${y}`;
    },"");
});



// to draw the zero value line wi get create a const yZeroLine
const yZeroLine = computed(() => {
    return amountToPixels(0)
});

const showLine = ref(false)

const lineShowedPosition = ref(0);

const emit = defineEmits(["selector", "returnZero"])

watch(lineShowedPosition, (value) => {
    const index = Math.ceil(value / (330 / (amounts.value.length - 1)));
    // if (index < 0 || index >= amounts.value.length) return;
    const theSelectedAmount = amounts.value[index - 1]
    emit("selector", theSelectedAmount);
});


const tapActive = ({ target, touches }) => {
    showLine.value = true;
    // console.log(target, touches); 
    const canvaWidth = target.getBoundingClientRect().width;
    const xPosition = target.getBoundingClientRect().x;
    const touchInX = touches[0].clientX;
    // console.log(canvaWidth, xPosition, touchInX);
    lineShowedPosition.value = ((touchInX - xPosition) * 330) / canvaWidth;
}

const untap = () => {
    showLine.value = false
    emit("returnZero")
}

const tapActiveClick = (canvas) => {
    showLine.value = true;
    console.log(canvas); 
    console.log(canvas.clientX); 

    const touchInX = canvas.clientX;
    console.log("touch in X" , touchInX); 

    const canvaWidth = canvas.srcElement.clientWidth;
    console.log("Canva width" , canvas.srcElement.clientWidth);

    const viewPortWidth = visualViewport.width;
    console.log("viewPortWidth  ==> " , viewPortWidth);

    const xPosition = (visualViewport.width - canvaWidth) / 2;
    console.log("X Position start", xPosition);

    lineShowedPosition.value = ((touchInX - xPosition) * 330) / canvaWidth;
}



</script>

<template>
    <div>
        <svg 
            viewBox="0 0 330 220"
            @touchstart="tapActive"
            @touchmove="tapActive"
            @touchend="untap"
            @click="tapActiveClick"
        >
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
                v-show="showLine" 
                stroke="green" 
                stroke-width="2"
                :x1="lineShowedPosition"
                y1="0"
                :x2="lineShowedPosition"
                y2="220"/>
        </svg>
        <p>Last 30 days</p>
        <p>{{ amounts }}</p>
        <!-- <p>{{ points  }}</p> -->
    </div>
</template>



<style scoped>
svg {
  /* width: 100%; */
  width: 75vw;
}
p {
  text-align: center;
}
</style>