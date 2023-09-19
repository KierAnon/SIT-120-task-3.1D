<script setup>
import { reactive } from 'vue';
import { state } from '../stateModule';
import { useRouter } from 'vue-router';

const router = useRouter();

const formData = reactive(
  {
    name: '',
    description: '',
    category: '',
    stats: [{ name: '', amount: '' }],
    image: null
  }
  )

const handleSubmit = (e) => {
  e.preventDefault();
  state.formData = formData
  router.push({ name: 'home' });

}

const addStat = () => {
  formData.stats.push({ name: '', amount: '' });
};

const removeStat = (index) => {
  formData.stats.splice(index, 1);
};

const handleFileUpload = (event) => {
  const file = event.target.files[0];
  if (file) {
    const reader = new FileReader();
    reader.onload = (e) => {
      formData.image = e.target.result;
    };
    reader.readAsDataURL(file);
  }
};
</script>

<template>
  <div class="view-container">
    <h1>Add an item</h1>
    <form class="form-container">
      <label for="name">Name of item</label>
      <input type="text" id="name" v-model="formData.name"/>

      <label for="description">Description</label>
      <input type="text" id="description" v-model="formData.description"/>

      <label for="category">Choose a category</label>
      <select name="category" id="category" v-model="formData.category">
        <option value="food" >Food</option>
        <option value="transportation">Transportation</option>
      </select>

      <div v-for="(stat, index) in formData.stats" :key="index" class="stats-group">
        <label :for="'stat-name-' + index">Stat Name</label>
        <input :id="'stat-name-' + index" type="text" v-model="stat.name" />
        
        <label :for="'stat-amount-' + index">Amount</label>
        <input :id="'stat-amount-' + index" type="text" v-model="stat.amount" />

        
      </div>
      <button type="button" @click="() => addStat(index)">Add another stat</button>
        <button type="button" @click="() => removeStat(index)">Remove stat</button>
      <br>
      <label for="image">Image</label>
      <input id="image" type="file" @change="handleFileUpload"/>
      <div v-if="formData.image">
        <img :src="formData.image" alt="Uploaded Image" />
      </div>

      <button @click="handleSubmit" type="submit">Submit</button>
    </form>
  </div>
</template>

<style scoped>
.view-container{
  margin: 0 auto;
  width: 80%;
}

h1{
  text-align: center;
  padding: 20px;
}

.form-container {
padding: 20px;
border: 1px solid #ccc;
border-radius: 5px;
}

label {
  display: block;
  margin-bottom: 5px;
}

input, textarea {
  width: 100%;
  padding: 8px;
  border: 1px solid #ccc;
  border-radius: 4px;
  box-sizing: border-box;
}

button {
  padding: 10px 15px;
  border: none;
  margin: 5px;
  border-radius: 4px;
  background-color: #28a745;
  color: #fff;
  cursor: pointer;

}

button:hover {
  background-color: #218838;
}
  </style>
  