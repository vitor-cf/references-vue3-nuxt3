<template>
  <div class="container">
    <h3>Validação de CPF utilizando InputMask do PrimeVue</h3>
    <div class="p-fluid p-field">
      <label for="cpf">CPF</label>
      <InputMask 
      type="text"
      v-model="cpf"
      mask="999.999.999-99" 
      @blur="validarCpf" 
      :class="{ 'is-invalid': isInvalid }" 
    />
    </div>
  </div>
</template>
<style scoped>
.is-invalid {
    border: 1px solid red;
}
</style>

<script setup>
const cpf = ref('');
const isInvalid = ref(false); 

function validarCPF(cpf) {
  cpf = cpf.replace(/[^\d]+/g,'');
  if(cpf == '') return false;
  // Elimina CPFs invalidos conhecidos
  if (cpf.length != 11 ||
    cpf == "00000000000" ||
    cpf == "11111111111" ||
    cpf == "22222222222" ||
    cpf == "33333333333" ||
    cpf == "44444444444" ||
    cpf == "55555555555" ||
    cpf == "66666666666" ||
    cpf == "77777777777" ||
    cpf == "88888888888" ||
    cpf == "99999999999")
      return false;
  // Valida 1o digito
  add = 0;
  for (i=0; i < 9; i ++)
    add += parseInt(cpf.charAt(i)) * (10 - i);
  rev = 11 - (add % 11);
  if (rev == 10 || rev == 11)
    rev = 0;
  if (rev != parseInt(cpf.charAt(9)))
    return false;
  // Valida 2o digito
  add = 0;
  for (i = 0; i < 10; i ++)
    add += parseInt(cpf.charAt(i)) * (11 - i);
  rev = 11 - (add % 11);
  if (rev == 10 || rev == 11)
    rev = 0;
  if (rev != parseInt(cpf.charAt(10)))
    return false;
  return true;
}

function validarCpf() {
  if (cpf.value) {
    isInvalid.value = !validarCPF(cpf.value);
  } 
}
</script>