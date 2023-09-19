<script setup>
import { reactive } from 'vue';
import { state } from '../stateModule';
import { useRouter } from 'vue-router';

const router = useRouter();

const formData = reactive(
  {
    name: '',
    description: ''
  }
  )

const handleSubmit = (e) => {
  e.preventDefault();
  state.formData = formData
  router.push({ name: 'home' });

}
</script>

<template>
  <div >
    <h1>Add an item</h1>
    <form class="form-container">
      <label for="name">Name of item</label>
      <input type="text" id="name" v-model="formData.name"/>

      <label for="description">Description</label>
      <input type="text" id="description" v-model="formData.description"/>

      <button @click="handleSubmit" type="submit">Submit</button>
    </form>
  </div>
</template>

<style scoped>
.form-container {
width: 300px;
margin: 0 auto;
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
  border-radius: 4px;
  background-color: #28a745;
  color: #fff;
  cursor: pointer;
}

button:hover {
  background-color: #218838;
}
  </style>
  