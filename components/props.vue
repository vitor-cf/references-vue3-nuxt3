<template>
    <div>
        <h1>Usando props</h1>
        <p>passe o titulo: {{ title }}</p>
    </div>
</template>

<script lang="ts" setup>
// Como passar props para linguagem typescript
// Passamos props como camelCase
defineProps<{
    title?: string
    likes?: number
}>()
</script>