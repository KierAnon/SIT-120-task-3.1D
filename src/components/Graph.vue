<script setup>
import { reactive, ref } from 'vue';

const props = defineProps({
    bars:{
        type: Array
    }
})

const showToolTip = ref(false);
let hoveredIndex = ref(null);
let tooltipPosition = reactive({x: 0, y: 0});

const handleMouseOver = (index, event) => {
    hoveredIndex.value = index;
    tooltipPosition.x = event.clientX;
    tooltipPosition.y = event.clientY;
}

const handleMouseOut = () => {
    hoveredIndex.value = null;
}

const handleMouseMove = (event) => {
    tooltipPosition.x = event.clientX;
    tooltipPosition.y = event.clientY;
}

// const barValue = ref(`${bar.amount}px`)

</script>

<template>
    <div v-for="(bar, index) in bars" :key="index" class="graph-container">
        <p>{{ bar.name }}</p>
        <svg width="200px" height="10">
            <rect 
                :width="bar.amount"
                height="10"
                style="fill:blue"
                @mouseover="(event) => handleMouseOver(index, event)"
                @mousemove="handleMouseMove"
                @mouseout="handleMouseOut"
            />
        </svg>
        <span v-if="hoveredIndex == index" class="hover-text" :style="{ left: `${tooltipPosition.x}px`, top: `${tooltipPosition.y}px` }">{{ bar.amount }}</span>
        
    </div>
    
</template>


<style scoped>
p{
    max-width: 50px;
    min-width: 50px;
}
.graph-container{
    display:flex;
    align-items: center;
    justify-content: flex-end;
}

.hover-text{
    position: fixed;
    background-color: white;
    border: 1px solid black;
    padding: 10px;
    pointer-events: none;
}



</style>