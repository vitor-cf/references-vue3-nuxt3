<template>
    <header>
        <nav>
            <ul>
                <li>
                    <NuxtLink to="about">About</NuxtLink>
                </li>
                <li>
                    <NuxtLink to="posts/edit/1">Post 1</NuxtLink>
                </li>
                <li>
                    <NuxtLink :to="nome" `>Post 2</NuxtLink>
                </li>
            </ul>
        </nav>
    </header>
</template>

<script setup>

let idProduto = "1";
const nome = `posts/${idProduto}`;
</script>