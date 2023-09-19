<script setup>
import { ref, toRef } from 'vue';
import Card from '../components/Card.vue';
import { state } from '../stateModule';

toRef(state);



const initalItems = [
  {
    title: 'Driving',
    description: 'The car is petrol powered and is an average 4 door sedan.',
    image: '/car.jpg',
    category: 'transportation',
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
    description: 'The bike is a standard road bike.',
    image: 'biking.webp',
    category: 'transportation',
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
    description: 'The electric vehicle is a Tesla Model 3.',
    image: 'ev.jpg',
    category: 'transportation',
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
    description: 'The steak was from a grass fed farm.',
    image: 'steak.jpg',
    category: 'food',
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

if(state.formData){
  console.log('output')
  console.log(state.name)
  console.log(state.formData)
  console.log(state.formData.name)
  const newItem = {
    title: state.formData.name,
    subtitle: 'blank',
    description: state.formData.description,
    image: '#',
    stats: [
      {
        name: 'carbon',
        amount: 20
      }
    ]
  }
  initalItems.push(newItem);
}

</script>

<template>
  <main class="home">
    <h1>Home</h1>
    <button class="button" @click="sortItems">Sort by carbon</button>
    <label for="category">Choose a category:</label>
    <select name="category" id="category">
      <option value="all">All</option>
      <option value="food">Food</option>
      <option value="transportation">Transportation</option>
      <option value="clothes">Clothes</option>
    </select>

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