<template>
    <div>
        <label for="cnpj">CNPJ:</label>
        <!-- Utilizei o @blur para validar ao tirar o focus do input :class adiciona a classe 
        'is-invalid' se o IsInvalid retornar true apos executar a função
        -->
        <InputMask 
        mask="99.999.999/9999-99" 
        type="text" 
        v-model="cnpj"
        @blur="validarCnpj" 
        :class="{ 'is-invalid': isInvalid }" 
        />
        <!-- <div v-if="isInvalid" class="invalid-feedback">CNPJ inválido.</div> -->
    </div>
</template>
<style scoped>
.is-invalid {
    border: 1px solid red;
  }
  
</style>
<script lang="ts" setup>
const cnpj = ref('');
const isInvalid = ref(false);

function validarCNPJ(cnpj:any) {
    
cnpj = cnpj.replace(/[^\d]+/g,'');

if(cnpj == '') return false;

if (cnpj.length != 14)
  return false;

// Elimina CNPJs invalidos conhecidos
if (cnpj == "00000000000000" ||
    cnpj == "11111111111111" ||
    cnpj == "22222222222222" ||
    cnpj == "33333333333333" ||
    cnpj == "44444444444444" ||
    cnpj == "55555555555555" ||
    cnpj == "66666666666666" ||
    cnpj == "77777777777777" ||
    cnpj == "88888888888888" ||
    cnpj == "99999999999999")
    return false;

// Valida DVs
let tamanho = cnpj.length - 2
let numeros = cnpj.substring(0,tamanho);
let digitos = cnpj.substring(tamanho);
let soma = 0;
let pos = tamanho - 7;

for (var i = tamanho; i >= 1; i--) {
  soma += numeros.charAt(tamanho - i) * pos--;
  if (pos < 2)
        pos = 9;
}
let resultado = soma % 11 < 2 ? 0 : 11 - soma % 11;
if (resultado != digitos.charAt(0))
    return false;

tamanho = tamanho + 1;
numeros = cnpj.substring(0,tamanho);
soma = 0;
pos = tamanho - 7;
for (i = tamanho; i >= 1; i--) {
  soma += numeros.charAt(tamanho - i) * pos--;
  if (pos < 2)
        pos = 9;
}
resultado = soma % 11 < 2 ? 0 : 11 - soma % 11;
if (resultado != digitos.charAt(1))
      return false;

return true;
}


function validarCnpj() {
  if (cnpj.value) {
    isInvalid.value = !validarCNPJ(cnpj.value);
  } 
}
</script>