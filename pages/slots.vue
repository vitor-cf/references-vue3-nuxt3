
import UsandoSlots from '~/components/usandoSlots.vue';

<template>
    <!-- O slot é onde podemos passar fragmentos, podemos inserir componentes, tags... -->
    <!-- Para utilizarmos o slot utilizamos a sintaxe abaixo -->
    <!-- Para utilizar mais de um slot, precisamos referência o slot e chama-lo pelo seu nome referenciado -->
    <div>
        <UsandoSlot>
            <h1>Usando um slot do componente</h1>
        </UsandoSlot>
    </div>
</template>