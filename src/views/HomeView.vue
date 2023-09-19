<script setup>
import { ref, toRef } from 'vue';
import Card from '../components/Card.vue';
import { state } from '../stateModule';

toRef(state);

const initialItems = [
  {
    title: 'Driving',
    description: 'Driving 1km in a petrol car',
    image: '/car.jpg',
    category: 'transportation',
    stats: [
      {
        name: "carbon",
        type: 'g',
        amount: 170
      }     
    ]
  },
  {
    title: 'Flying',
    description: 'Flying 1km in a plane',
    image: '/flying.gif',
    category: 'transportation',
    stats: [
      {
        name: "carbon",
        type: 'g',
        amount: 246
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
        type: 'g',
        amount: 47
      }     
    ]
  },
  {
    title: 'Bus',
    description: 'Travelling 1km in a bus',
    image: 'bus.jpg',
    category: 'transportation',
    stats: [
      {
        name: "carbon",
        type: 'g',
        amount: 97
      }    
    ]
  },
  {
    title: 'Eating a steak',
    description: '100 grams of beef',
    image: 'steak.jpg',
    category: 'food',
    stats: [
      {
        name: "carbon",
        amount: 9900
      }     
    ]
  },
  {
    title: 'Tofu',
    description: '100 grams of tofu',
    image: 'tofu.jpg',
    category: 'food',
    stats: [
      {
        name: "carbon",
        amount: 320
      }    
    ]
  }
]

const filterItems = (chosenFilter) => {
  if(chosenFilter.target.value == 'all'){
    items.value = initialItems;
  }else{
    const filteredItems = initialItems.filter((item) => item.category == chosenFilter.target.value);
    items.value = filteredItems;
  }
  
  
}

let items = ref(initialItems);
const category = ref('all');

const sortItems = () => {
  items.value.sort((a, b) =>
    b.stats.find(stat => stat.name === "carbon").amount - 
    a.stats.find(stat => stat.name === "carbon").amount
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
    description: state.formData.description,
    category: state.formData.category,
    image: state.formData.image,
    stats: state.formData.stats
  }
  initialItems.push(newItem);
}

</script>

<template>
  <main class="home">
    <h1>Home</h1>
    <div class="controls">
      <div>
    <button class="button" @click="sortItems">Sort by carbon</button>
    </div>
    <div>
      <label for="category">Choose a category:</label>
      <select name="category" id="category" v-model="category" @change="filterItems($event)">
        <option value="all">All</option>
        <option value="food">Food</option>
        <option value="transportation">Transportation</option>
        <option value="clothes">Clothes</option>
      </select>
    </div>
    </div>

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
.home {
    padding: 20px;
    width: 90%;
    margin: 0 auto;
}

h1 {
    text-align: center;
    color: #333;
    margin-bottom: 20px;
}

.button {
    padding: 10px 20px;
    font-size: 16px;
    color: #fff;
    background-color: #28a745;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    margin: 0 10px;
}

.button:hover {
    background-color: #218838;
}

.controls{
  display: flex;
  justify-content: space-between;
}

label {
    font-size: 16px;
    color: #333;
    display: block;
    margin-bottom: 8px;
}

select {
    padding: 8px;
    font-size: 16px;
    border: 1px solid #ccc;
    border-radius: 5px;
}

.home-container{
  display: flex;
  flex-grow: 1;
  flex-wrap: wrap;
}

.card-item{
  flex: 1 1 0;
}


</style>