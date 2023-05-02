<template>
    <div class="p-m-4">
        <h3 class="p-mb-3">Tabela com botão na última coluna</h3>
        <ClientOnly>
            <DataTable :value="cars" dataKey="id">
                <Column field="vin" header="Vin"></Column>
                <Column field="brand" header="Brand"></Column>
                <Column header="Options">
                    <template #body="rowData">
                        <div>
                            <button @click="showOptions(rowData)"> CLICK </button>
                            <div v-if="rowData.showOptions">
                                <p>Option 1</p>
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
  
<script setup>
import { ref } from 'vue'
const cars = ref([
    { id: 1, vin: '123456789', brand: 'Toyota', showOptions: false },
    { id: 2, vin: '987654321', brand: 'Honda', showOptions: false }
]);


function showOptions(rowData) {
    rowData.showOptions = !rowData.showOptions;
}
</script>