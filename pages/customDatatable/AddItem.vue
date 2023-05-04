<template>
    <div class="p-m-4">
        <div class="flex">
            <InputText class="border border-slate-950" placeholder="adicione vin" v-model="carsAdicionado.vin" />
            <InputText class="ml-2 border border-slate-950" placeholder="adicione brand" v-model="carsAdicionado.brand" />
            <div>
                <button class="ml-2 bg-gray-800 text-white p-2 rounded-full" @click="addCars(cars, carsAdicionado)">+
                    Adicione</button>
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
const cars = reactive([]);

const carsAdicionado = reactive({
    vin: "",
    brand: "",
});
interface Dados {
    vin: string,
    brand: string
}
const addCars = (arrayMain: Array<object>, newDatas: Dados) => {
    // adicionar um novo objeto ao array 
    arrayMain.push({
        ...newDatas
    });
}

</script>