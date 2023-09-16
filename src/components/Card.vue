<script setup>
import { ref } from 'vue';

const props = defineProps({
    title: {
      type: String,
      required: true
    },
    subtitle: {
      type: String,
      default: ''
    },
    description: {
      type: String,
      default: ''
    },
    image: {
        type: String
    },
    stats:{
        type: Object
    }
})

const barValue = ref(`${props.stats[0].amount}px`)

</script>

<template>
<div class="card">
    <div class="card-header">
      <h2>{{ title }}</h2>
      <h5>{{ subtitle }}</h5>
    </div>
    <div class="card-body">
        <img :src="image" />
      <p>{{ description }}</p>
      <div class="bar-chart-container">
        <div class="bar-container">
            <p>{{ stats[0].name }}</p>
            <div class="bar" :style="{width: barValue}" ></div>

        </div>
      </div>
    </div>
</div>
</template>


<style>
.card {
  border: 1px solid #e0e0e0;
  border-radius: 8px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
  padding: 16px;
  max-width: 300px;
  margin: 16px;
}

.bar-chart-container {
    display: flex;
    align-items: flex-end;
    background-color: #f9f9f9;
    padding: 10px;
    border: 1px solid #ccc;
}

.bar-container{
    display: flex;
    align-items: center;
}

.bar {
    height: 10px;
    margin: 0 5px;
    max-width: 200px;
    background-color: #76c7c0;
 }

</style>