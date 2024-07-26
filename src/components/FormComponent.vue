<script setup>
import { ref, watch, defineProps, defineEmits } from 'vue'

const props = defineProps({
  initialForms: {
    type: Object,
    required: true,
  },
  states: {
    type: Array,
    required: true,
  },
})

const emit = defineEmits(['onSubmit'])


// Decompoe o initialForms que está no props
const localForms = ref({ ...props.initialForms })

watch(localForms, (newForms) => {
  emit('onSubmit', newForms)
})

function onSubmit() {
  emit('onSubmit', localForms.value)
}

function handleAvatarChange(event) {
  const file = event.target.files[0]
  const reader = new FileReader()
  reader.onload = (e) => {
    localForms.value.avatar = e.target.result
  }
  reader.readAsDataURL(file)
}
</script>


<template>
  <form @submit.prevent="onSubmit" class="form">
    <fieldset class="fieldset">
      <legend>Dados pessoais</legend>
      <div class="form-group">
        <label for="nome">Nome:</label>
        <input
          type="text"
          id="nome"
          v-model="localForms.nome"
          placeholder="Digite seu nome"
          required
        />
      </div>

      <div class="form-group">
        <label for="email">Email:</label>
        <input
          type="email"
          id="email"
          v-model="localForms.email"
          placeholder="Digite seu email"
          required
        />
      </div>

      <div class="form-group">
        <label for="password">Senha:</label>
        <input
          type="password"
          id="password"
          v-model="localForms.senha"
          placeholder="Digite sua senha"
          required
        />
      </div>

      <div class="form-group">
        <label for="confirmarSenha">Confirmar Senha:</label>
        <input
          type="password"
          id="confirmarSenha"
          v-model="localForms.confirmarSenha"
          placeholder="Confirme sua senha"
          required
        />
      </div>

      <div class="form-group">
        <label for="dataNascimento">Data de Nascimento:</label>
        <input type="date" id="dataNascimento" v-model="localForms.dataNascimento" required />
      </div>

      <div class="form-group">
        <label for="hobbies">Hobbies:</label>
        <input
          type="text"
          id="hobbies"
          v-model="localForms.hobbies"
          placeholder="Hobbies"
          required
        />
      </div>

      <div class="form-group">
        <label>Linguagens de Programação Preferida:</label>
        <div class="radio-group">
          <input type="radio" id="langC" v-model="localForms.linguagemProg" value="C" />
          <label for="langC">C</label>

          <input type="radio" id="langJava" v-model="localForms.linguagemProg" value="Java" />
          <label for="langJava">Java</label>

          <input type="radio" id="langPython" v-model="localForms.linguagemProg" value="Python" />
          <label for="langPython">Python</label>

          <input type="radio" id="langJs" v-model="localForms.linguagemProg" value="JavaScript" />
          <label for="langJs">JavaScript</label>
        </div>
      </div>

      <div class="form-group">
        <label for="avatar">Avatar:</label>
        <input
          type="file"
          id="avatar"
          @change="handleAvatarChange"
          accept="image/*"
        />
      </div>

      <div class="form-group">
        <label for="biografia">Biografia:</label>
        <textarea
          name="biografia"
          id="biografia"
          v-model="localForms.biografia"
          placeholder="Conte um pouco sobre você"
          required
        ></textarea>
      </div>
    </fieldset>

    <fieldset class="fieldset">
      <legend>Endereço</legend>
      <div class="form-group">
        <label for="estado">Estado:</label>
        <select id="estado" v-model="localForms.estado" required>
          <option disabled value="">Selecione um estado</option>
          <option v-for="state in states" :key="state.uf" :value="state.uf">{{ state.name }}</option>
        </select>
      </div>
      <div class="form-group">
        <label for="cidade">Cidade:</label>
        <input type="text" id="cidade" v-model="localForms.cidade" :disabled="!localForms.estado" placeholder="Escolha um estado primeiro" required />
      </div>
      <div class="box-btn">
        <button type="submit">Enviar</button>
      </div>
    </fieldset>
  </form>
</template>


<style scoped>

</style>
