<script setup>
import { reactive, ref, computed } from 'vue'

const MAX_BIO = 200

const cursos = ['Ciência da Computação', 'Sistemas de Informação', 'Engenharia de Software', 'Design', 'Outro']
const opcoesInteresses = ['Front-end', 'Back-end', 'Mobile', 'UI/UX', 'Dados', 'DevOps']

const form = reactive({
  nome: '',
  email: '',
  curso: '',
  semestre: '',
  interesses: [],
  bio: ''
})

const erros = reactive({})
const sucesso = ref(false)

const restantes = computed(() => MAX_BIO - form.bio.length)

function validar() {
  // limpa erros anteriores
  Object.keys(erros).forEach((k) => delete erros[k])

  if (!form.nome.trim()) erros.nome = 'O nome é obrigatório.'

  const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/
  if (!form.email.trim()) erros.email = 'O e-mail é obrigatório.'
  else if (!emailRegex.test(form.email)) erros.email = 'Digite um e-mail válido.'

  if (!form.curso) erros.curso = 'Selecione um curso.'

  if (!form.semestre || form.semestre < 1 || form.semestre > 12)
    erros.semestre = 'Informe um semestre entre 1 e 12.'

  if (form.interesses.length === 0) erros.interesses = 'Escolha pelo menos um interesse.'

  return Object.keys(erros).length === 0
}

function enviar() {
  sucesso.value = false
  if (!validar()) return

  console.log('Cadastro enviado:', JSON.parse(JSON.stringify(form)))
  sucesso.value = true

  // limpa os campos
  form.nome = ''
  form.email = ''
  form.curso = ''
  form.semestre = ''
  form.interesses = []
  form.bio = ''
}
</script>

<template>
  <main class="container">
    <h1>Cadastro de Novo Membro</h1>

    <p v-if="sucesso" class="sucesso">✅ Cadastro realizado com sucesso!</p>

    <form class="form" @submit.prevent="enviar" novalidate>
      <!-- Nome -->
      <label>
        Nome completo
        <input type="text" v-model="form.nome" placeholder="Seu nome" />
        <span v-if="erros.nome" class="erro">{{ erros.nome }}</span>
      </label>

      <!-- E-mail -->
      <label>
        E-mail
        <input type="email" v-model="form.email" placeholder="voce@email.com" />
        <span v-if="erros.email" class="erro">{{ erros.email }}</span>
      </label>

      <!-- Curso -->
      <label>
        Curso / Área de atuação
        <select v-model="form.curso">
          <option value="" disabled>Selecione...</option>
          <option v-for="c in cursos" :key="c" :value="c">{{ c }}</option>
        </select>
        <span v-if="erros.curso" class="erro">{{ erros.curso }}</span>
      </label>

      <!-- Semestre -->
      <label>
        Semestre / Período
        <input type="number" min="1" max="12" v-model.number="form.semestre" />
        <span v-if="erros.semestre" class="erro">{{ erros.semestre }}</span>
      </label>

      <!-- Interesses -->
      <fieldset>
        <legend>Interesses / Habilidades</legend>
        <label v-for="i in opcoesInteresses" :key="i" class="check">
          <input type="checkbox" :value="i" v-model="form.interesses" />
          {{ i }}
        </label>
        <span v-if="erros.interesses" class="erro">{{ erros.interesses }}</span>
      </fieldset>

      <!-- Bio -->
      <label>
        Mensagem / Bio curta
        <textarea v-model="form.bio" :maxlength="MAX_BIO" rows="4" />
        <small>{{ restantes }} caracteres restantes</small>
      </label>

      <button type="submit">Enviar cadastro</button>
    </form>
  </main>
</template>

<style scoped>
.container {
  max-width: 600px;
  margin: 24px auto;
  padding: 24px;
  background: #fff;
  border-radius: 8px;
}
.form {
  display: flex;
  flex-direction: column;
  gap: 16px;
}
label {
  display: flex;
  flex-direction: column;
  gap: 4px;
  font-weight: bold;
}
input,
select,
textarea {
  padding: 8px;
  border: 1px solid #ccc;
  border-radius: 4px;
  font-size: 1rem;
  font-weight: normal;
}
fieldset {
  border: 1px solid #ccc;
  border-radius: 4px;
  display: flex;
  flex-wrap: wrap;
  gap: 12px;
}
.check {
  flex-direction: row;
  align-items: center;
  font-weight: normal;
}
button {
  padding: 12px;
  background: #2563eb;
  color: #fff;
  border: none;
  border-radius: 4px;
  font-size: 1rem;
  cursor: pointer;
}
button:hover {
  background: #1d4ed8;
}
.erro {
  color: #dc2626;
  font-size: 0.85rem;
  font-weight: normal;
}
.sucesso {
  padding: 12px;
  background: #dcfce7;
  color: #166534;
  border-radius: 4px;
}

/* Responsividade */
@media (max-width: 480px) {
  .container {
    margin: 0;
    border-radius: 0;
  }
}
</style>