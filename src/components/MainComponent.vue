<script setup>
import { ref } from 'vue'
import FormComponent from '@/components/FormComponent.vue'
import ProfileComponent from '@/components/ProfileComponent.vue'

const Forms = ref({
  nome: '',
  email: '',
  senha: '',
  confirmarSenha: '',
  dataNascimento: '',
  endereco: '',
  cidade: '',
  estado: '',
  hobbies: '',
  linguagemProg: '',
  biografia: '',
  avatar: ''
})

const mostrarPerfil = ref(false)

const states = [
  { uf: 'AC', name: 'Acre' },
  { uf: 'AL', name: 'Alagoas' },
  { uf: 'AP', name: 'Amapá' },
  { uf: 'AM', name: 'Amazonas' },
  { uf: 'BA', name: 'Bahia' },
  { uf: 'CE', name: 'Ceará' },
  { uf: 'DF', name: 'Distrito Federal' },
  { uf: 'ES', name: 'Espírito Santo' },
  { uf: 'GO', name: 'Goiás' },
  { uf: 'MA', name: 'Maranhão' },
  { uf: 'MT', name: 'Mato Grosso' },
  { uf: 'MS', name: 'Mato Grosso do Sul' },
  { uf: 'MG', name: 'Minas Gerais' },
  { uf: 'PA', name: 'Pará' },
  { uf: 'PB', name: 'Paraíba' },
  { uf: 'PR', name: 'Paraná' },
  { uf: 'PE', name: 'Pernambuco' },
  { uf: 'PI', name: 'Piauí' },
  { uf: 'RJ', name: 'Rio de Janeiro' },
  { uf: 'RN', name: 'Rio Grande do Norte' },
  { uf: 'RS', name: 'Rio Grande do Sul' },
  { uf: 'RO', name: 'Rondônia' },
  { uf: 'RR', name: 'Roraima' },
  { uf: 'SC', name: 'Santa Catarina' },
  { uf: 'SP', name: 'São Paulo' },
  { uf: 'SE', name: 'Sergipe' },
  { uf: 'TO', name: 'Tocantins' }
]

function validarForms(newForms) {
  Forms.value = newForms

  if (
    !Forms.value.nome ||
    !Forms.value.email ||
    !Forms.value.senha ||
    !Forms.value.confirmarSenha ||
    !Forms.value.dataNascimento ||
    !Forms.value.hobbies ||
    !Forms.value.linguagemProg ||
    !Forms.value.biografia ||
    !Forms.value.estado ||
    !Forms.value.cidade
  ) {
    alert('Por favor, preencha todos os campos obrigatórios.')
    return
  }

  if (Forms.value.senha !== Forms.value.confirmarSenha) {
    alert('As senhas não correspondem. Por favor, verifique.')
    return
  }

  mostrarPerfil.value = true
}
</script>

<template>
  <div class="container">
    <h1>Editor de Perfil</h1>
    <transition name="form" mode="out-in">
      <div :key="mostrarPerfil">
        <ProfileComponent v-if="mostrarPerfil" :forms="Forms" @onHide="mostrarPerfil = false" />
        <FormComponent v-else :initialForms="Forms" :states="states" @onSubmit="validarForms" />
      </div>
    </transition>
  </div>
</template>

<style scoped>

</style>