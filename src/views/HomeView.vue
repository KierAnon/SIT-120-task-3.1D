<script setup>
import { ref } from 'vue';
import Card from '../components/Card.vue';
const initalItems = [
  {
    title: 'Driving',
    subtitle: 'Driving 1 km in a standard vehicle',
    description: 'The car is petrol powered and is an average 4 door sedan.',
    image: '/car.jpg',
    stats: [
      {
        name: "carbon",
        amount: 280
      },
      {
        name: "calories",
        amount: 0
      }      
    ]
  },
  {
    title: 'Riding a bike',
    subtitle: 'Riding 1 km on a bike',
    description: 'The bike is a standard road bike.',
    image: 'biking.webp',
    stats: [
      {
        name: "carbon",
        amount: 1
      },
      {
        name: "calories",
        amount: 50
      }      
    ]
  },
  {
    title: 'Driving an EV',
    subtitle: 'Driving 1 km in a standard vehicle',
    description: 'The electric vehicle is a Tesla Model 3.',
    image: 'ev.jpg',
    stats: [
      {
        name: "carbon",
        amount: 30
      },
      {
        name: "calories",
        amount: 0
      }      
    ]
  },
  {
    title: 'Eating a steak',
    subtitle: 'Eating a 250gram steak',
    description: 'The steak was from a grass fed farm.',
    image: 'steak.jpg',
    stats: [
      {
        name: "carbon",
        amount: 280
      },
      {
        name: "calories",
        amount: 500
      }      
    ]
  }
]



let items = ref(initalItems);

const sortItems = () => {
  items.value.sort((a, b) =>
    a.stats.find(stat => stat.name === "carbon").amount - 
    b.stats.find(stat => stat.name === "carbon").amount
  );
  console.log(items.value)
}

</script>

<template>
  <main class="home">
    <h1>Home</h1>
    <button class="button" @click="sortItems">Sort by carbon</button>

    <div class="home-container">
    <Card class="card-item" v-for="(item, index) in items"
      :key="item.title"
      :title="item.title"
      :subtitle="item.subtitle"
      :description="item.description"
      :stats="item.stats"
      :image="item.image"
    />
  </div>
  </main>
</template>

<style>
.home-container{
  display: flex;
  flex-grow: 1;
  flex-wrap: wrap;
}

.card-item{
  flex: 1 1 0;
}


</style>