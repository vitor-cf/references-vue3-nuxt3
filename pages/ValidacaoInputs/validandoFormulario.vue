<template>
    <div>
        <form @submit.prevent="submitForm">
            <div>
                <label>Nome</label>
                <InputText
                placeholder="Digite seu nome"
                v-model="nome"
                :class="{'is-invalid': isInvalid}"
                maxlength="8"
                />
            </div>
            <div>
                <label>Sobrenome</label>
                <InputText
                placeholder="Digite seu sobrenome"
                v-model="sobrenome"
                :class="{'is-invalid': isInvalid}"
                />
            </div>
            <div>
                <label>Numero</label>
                <InputNumber
                placeholder="Digite um numero"
                v-model="numero"
                :class="{'is-invalid': isInvalid}"
                :useGrouping="false"
                />
            </div>
            <label>cnpj</label>
            <InputMask 
        mask="99.999.999/9999-99" 
        v-model="cnpj"
        @blur="validarCnpj" 
        :class="{ 'is-invalid': cnpjInvalid }" 
        />
            <button >Enviar</button>
        </form>
    </div>
</template>


<script setup>
// validando input cpf
const cnpj = ref('');
const cnpjInvalid = ref(false);
const nome = ref('')
const sobrenome = ref('');
const numero = ref();
function validarCNPJ(cnpj) {
    
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
    cnpjInvalid.value = !validarCNPJ(cnpj.value);
  } 
}

function submitForm() {
    if(validarCNPJ(cnpj.value)) {
        alert('Formulário enviado com sucesso!');
        cnpj.value='';
    } else {
        alert('Por favor, corrija o CPF antes de enviar o formuário!')
    }
}
</script> 

<style scoped>
.is-invalid {
    border: 1px solid red;
}
</style>