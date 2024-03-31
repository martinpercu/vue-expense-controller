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
                points="0,0 110,110 220,100 330,220"
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