<template>
    <span>Nome diferente do arquivo</span>
    <h1>recebeu id pela url</h1>
</template>

<script setup>
const route = useRoute()
// When accessing /posts/1, route.params.id will be 1
console.log(route.params.id)
</script>