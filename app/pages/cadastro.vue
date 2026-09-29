<template>
  <div class="min-h-screen bg-base-200 py-10 px-4">
    <div class="card bg-base-100 shadow-xl max-w-2xl mx-auto">
      <form class="card-body" novalidate @submit.prevent="enviarFormulario">
        <h1 class="card-title text-3xl">Cadastro</h1>
        <p class="text-base-content/70">Preencha seus dados para se cadastrar.</p>

        <!-- Mensagem de sucesso -->
        <div v-if="sucesso" role="alert" class="alert alert-success">
          <span>Cadastro realizado com sucesso!</span>
        </div>

        <!-- Nome completo -->
        <fieldset class="fieldset">
          <label class="fieldset-legend" for="nome">Nome completo *</label>
          <input
            id="nome"
            v-model="form.nome"
            type="text"
            class="input w-full"
            :class="{ 'input-error': erros.nome }"
            placeholder="Digite seu nome completo"
          >
          <p v-if="erros.nome" class="text-error text-sm">{{ erros.nome }}</p>
        </fieldset>

        <!-- E-mail -->
        <fieldset class="fieldset">
          <label class="fieldset-legend" for="email">E-mail *</label>
          <input
            id="email"
            v-model="form.email"
            type="email"
            class="input w-full"
            :class="{ 'input-error': erros.email }"
            placeholder="seuemail@exemplo.com"
          >
          <p v-if="erros.email" class="text-error text-sm">{{ erros.email }}</p>
        </fieldset>

        <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
          <!-- Curso / Área de atuação -->
          <fieldset class="fieldset">
            <label class="fieldset-legend" for="curso">Curso / Área de atuação *</label>
            <select
              id="curso"
              v-model="form.curso"
              class="select w-full"
              :class="{ 'select-error': erros.curso }"
            >
              <option value="" disabled>Selecione um curso</option>
              <option v-for="curso in cursos" :key="curso" :value="curso">{{ curso }}</option>
            </select>
            <p v-if="erros.curso" class="text-error text-sm">{{ erros.curso }}</p>
          </fieldset>

          <!-- Semestre / Período -->
          <fieldset class="fieldset">
            <label class="fieldset-legend" for="periodo">Semestre / Período *</label>
            <select
              id="periodo"
              v-model="form.periodo"
              class="select w-full"
              :class="{ 'select-error': erros.periodo }"
            >
              <option value="" disabled>Selecione o período</option>
              <option v-for="n in 10" :key="n" :value="n">{{ n }}º período</option>
            </select>
            <p v-if="erros.periodo" class="text-error text-sm">{{ erros.periodo }}</p>
          </fieldset>
        </div>

        <!-- Interesses / Habilidades -->
        <fieldset class="fieldset">
          <legend class="fieldset-legend">Interesses / Habilidades</legend>
          <div class="grid grid-cols-2 sm:grid-cols-3 gap-2">
            <label v-for="interesse in opcoesInteresses" :key="interesse" class="label cursor-pointer">
              <input
                v-model="form.interesses"
                type="checkbox"
                class="checkbox checkbox-primary"
                :value="interesse"
              >
              {{ interesse }}
            </label>
          </div>
        </fieldset>

        <!-- Mensagem / Bio curta -->
        <fieldset class="fieldset">
          <label class="fieldset-legend" for="bio">Mensagem / Bio curta</label>
          <textarea
            id="bio"
            v-model="form.bio"
            class="textarea w-full h-28"
            :maxlength="limiteBio"
            placeholder="Conte um pouco sobre você"
          />
          <p class="label justify-end">{{ form.bio.length }} / {{ limiteBio }} caracteres</p>
        </fieldset>

        <div class="card-actions justify-between items-center mt-2">
          <NuxtLink to="/" class="btn btn-ghost">Voltar</NuxtLink>
          <button type="submit" class="btn btn-primary">Cadastrar</button>
        </div>
      </form>
    </div>
  </div>
</template>

<script setup>
const cursos = [
  'Análise e Desenvolvimento de Sistemas',
  'Ciência da Computação',
  'Engenharia de Software',
  'Sistemas de Informação',
  'Outro',
]

const opcoesInteresses = ['Front-end', 'Back-end', 'Mobile', 'UI/UX', 'DevOps']

const limiteBio = 200

// Dados do formulário (ligados aos campos com v-model)
const form = reactive({
  nome: '',
  email: '',
  curso: '',
  periodo: '',
  interesses: [],
  bio: '',
})

// Mensagens de erro de cada campo
const erros = reactive({
  nome: '',
  email: '',
  curso: '',
  periodo: '',
})

const sucesso = ref(false)

function validarFormulario () {
  const emailValido = /^[^\s@]+@[^\s@]+\.[^\s@]+$/

  erros.nome = form.nome.trim() ? '' : 'O nome é obrigatório.'

  if (!form.email.trim()) {
    erros.email = 'O e-mail é obrigatório.'
  } else if (!emailValido.test(form.email.trim())) {
    erros.email = 'Digite um e-mail válido.'
  } else {
    erros.email = ''
  }

  erros.curso = form.curso ? '' : 'Selecione um curso.'
  erros.periodo = form.periodo ? '' : 'Selecione o período.'

  // Válido quando nenhum campo tem mensagem de erro
  return !erros.nome && !erros.email && !erros.curso && !erros.periodo
}

function limparFormulario () {
  form.nome = ''
  form.email = ''
  form.curso = ''
  form.periodo = ''
  form.interesses = []
  form.bio = ''
}

function enviarFormulario () {
  sucesso.value = false

  if (!validarFormulario()) {
    return
  }

  console.log('Dados do cadastro:', { ...form, interesses: [...form.interesses] })

  sucesso.value = true
  limparFormulario()
}
</script>
