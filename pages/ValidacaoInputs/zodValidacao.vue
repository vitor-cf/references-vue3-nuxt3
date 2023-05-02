<template>
  <form @submit.prevent="submitForm">
    <div>
      <label for="name">Name:</label>
      <input id="name" v-model="forms.name">
    </div>

    <div>
      <label for="email">Email:</label>
      <input id="email" v-model="forms.email">
    </div>

    <div>
      <label for="password">Password:</label>
      <input id="password" type="password" v-model="forms.password">
    </div>

    <button type="submit">Submit</button>
  </form>
</template>
  
<script lang="ts" setup>
import { z } from 'zod';

const forms = ref({
  name: "",
  email: "",
  password: ""
});

const schema = z.object({
  name: z.string().min(2).max(50),
  email: z.string().email().nonempty({
    message: "email obrigatório"
  }),
  password: z.string().min(8),
})

function submitForm() {

}

</script>