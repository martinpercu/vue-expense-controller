<script setup>
import { toRefs } from 'vue';
const props = defineProps({
    title: {
        type: String,
    }
});

const { title } = toRefs(props)
</script>
<template>
    <div class="expense">
        {{ title }}        
    </div>
</template>