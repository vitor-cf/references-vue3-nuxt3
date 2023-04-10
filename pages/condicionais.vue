<template>
    <div>
        <!-- O v-if se colocarmos um valor booleano false ele não renderiza apenas quando retornado true -->
        <button @click="toggleShow">Toggle show</button>
        <p v-if="show">Hello world</p>
        <!-- Utilizando o v-if para inserir um estilo utilizando atributo :class do vue -->
        <div v-if="isVisible" :class="{ active: isActive }">
            <p>{{ message }}</p>
        </div>
    </div>
</template>

<script setup>
import { ref } from 'vue';
const message = ref('teste');
const isActive = ref(true);
const isVisible = ref(true);
const show = ref(true);
const input = ref("");
let loginIncorreto = ref(false);

function toggleShow() {
    show.value = !show.value;
}

</script>

<style scoped>
* {
    margin: 0;
    padding: 0;
}

/* p {
    max-width: 5.7%;
    min-height: 5rem;
    background-color: blue;
} */

.mudarcor {
    border-color: 1px solid red;
}
</style>