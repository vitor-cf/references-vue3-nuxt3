<template>
    <div class="p-m-4">
        <div class="flex">
            <InputText class="border border-slate-950" placeholder="adicione vin" v-model="carsAdicionado.vin" />
            <InputText class="ml-2 border border-slate-950" placeholder="adicione brand" v-model="carsAdicionado.brand" />
            <div>
                <button class="ml-2 bg-gray-800 text-white p-2 rounded-full"
                    @click="addCars(carsAdicionado.vin, carsAdicionado.brand, cars.length, cars)">+ Adicione</button>
            </div>
        </div>
        <h3 class="p-mb-3">Tabela com botão na última coluna</h3>
        <ClientOnly>
            <DataTable :value="cars" dataKey="id">
                <Column field="vin" header="Vin"></Column>
                <Column field="brand" header="Brand"></Column>

            </DataTable>
        </ClientOnly>
    </div>
</template>
  
<script lang="ts" setup>
import { ref } from 'vue'
const cars = ref<[{ id: number; vin: string; brand: string; }][]>([]);

const carsAdicionado = reactive({
    id: 1,
    vin: "",
    brand: "",
});
const addCars = (placa: string, marca: string, quantidade: number, arrayMain: Array<object>) => {
    // adicionar um novo objeto ao array 
    arrayMain.push({
        id: quantidade + 1,
        vin: placa,
        brand: marca
    });
    // Limpa o objeto dos novos dados
    placa = "",
        marca = ""
}

</script>