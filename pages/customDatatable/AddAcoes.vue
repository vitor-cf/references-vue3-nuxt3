<template>
    <div class="p-m-4">
        <h3 class="p-mb-3">Tabela com botão na última coluna</h3>
        <ClientOnly>
            <DataTable :value="cars" dataKey="id">
                <Column field="vin" header="Vin"></Column>
                <Column field="brand" header="Brand"></Column>
                <Column header="Options">
                    <template #body="slotProps">
                        <div>
                            <button @click="showOptions(slotProps.data)"> CLICK </button>
                            <div v-show="slotProps.data.showOptions">
                                <NuxtLink :to="passandoIdRota(cars[slotProps.index].id)">teste</NuxtLink>
                                <p>Option 2</p>
                                <p>Option 3</p>
                            </div>
                        </div>
                    </template>
                </Column>
            </DataTable>
        </ClientOnly>
    </div>
</template>
  
<script lang="ts" setup>
// Dados para popular o datatable
const cars = reactive([
    { id: 10923810913, vin: '123456789', brand: 'Toyota', showOptions: false },
    { id: 13124124121, vin: '987654321', brand: 'Honda', showOptions: false }
]);
// interface para verificar tipo de dados
interface Dados {
    id: number,
    vin: string,
    brand: string,
    showOptions: boolean
}
// function para pegar o valor unido de da linha selecionado e envia junto da url
const passandoIdRota = (id: number) => {
    return `/passandoidrota/posts/${id}`
}
// function para mostrar as options na tabela referente a linha
function showOptions(rowData: Dados) {
    rowData.showOptions = !rowData.showOptions;
}
</script>