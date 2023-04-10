<template>
    <form @submit.prevent="submitForm">
      <div>
        <label for="name">Name:</label>
        <input id="name" v-model="name">
        <p v-if="nameError">{{ nameError }}</p>
      </div>
  
      <div>
        <label for="email">Email:</label>
        <input id="email" v-model="email">
        <p v-if="emailError">{{ emailError }}</p>
      </div>
  
      <div>
        <label for="password">Password:</label>
        <input id="password" type="password" v-model="password">
        <p v-if="passwordError">{{ passwordError }}</p>
      </div>
  
      <button type="submit">Submit</button>
    </form>
  </template>
  
  <script lang="ts" setup>
  import { ref } from 'vue'
  import { z } from 'zod';
  
  const schema = z.object({
    name: z.string().min(2).max(50),
    email: z.string().email(),
    password: z.string().min(8),
  })
  
  const name = ref('')
  const email = ref('')
  const password = ref('')
  const nameError = ref('')
  const emailError = ref('')
  const passwordError = ref('')
  
  const submitForm = () => {
    const data = {
      name: name.value,
      email: email.value,
      password: password.value,
    }
  
    try {
      schema.validateSync(data)
      // Form is valid, do something with data
    } catch (error) {
      // Form is invalid, display error messages
      nameError.value = error.errors?.find(e => e.path[0] === 'name')
      emailError.value = error.errors?.find(e => e.path[0] === 'email')
      passwordError.value = error.errors?.find(e => e.path[0] === 'password')
    }
  }
  </script>