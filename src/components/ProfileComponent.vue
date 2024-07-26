<script setup>
import { toRefs } from 'vue'

const props = defineProps({
  forms: Object,
})

const { forms } = toRefs(props)

// toRefs deixa um objeto reativo separados 
</script>


<template>
    <fieldset class="fieldset">
      <legend>Perfil</legend>
      <div class="form-group">
        <img v-if="forms.avatar" class="avatar" :src="forms.avatar" />
        <p><strong>Nome:</strong> {{ forms.nome }}</p>
        <p><strong>Email:</strong> {{ forms.email }}</p>
        <p><strong>Data de Nascimento:</strong> {{ forms.dataNascimento }}</p>
        <p><strong>Hobbies:</strong> {{ forms.hobbies }}</p>
        <p><strong>Linguagem de Programação Preferida:</strong> {{ forms.linguagemProg }}</p>
        <p><strong>Biografia:</strong> {{ forms.biografia }}</p>
        <p><strong>Endereço:</strong> {{ forms.cidade }}, {{ forms.estado }}</p>
      </div>
      <div class="box-btn">
        <button @click="$emit('onHide')">Voltar</button>
      </div>
    </fieldset>
  </template>
  
<style scoped>

  </style>
  