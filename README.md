# Atividade - Node.js + Vue.js + Nuxt

Projeto acadêmico baseado no repositório [nuxt-youtube](https://github.com/patrickmonteiro/nuxt-youtube).
O objetivo é praticar o sistema de rotas do Nuxt criando uma nova página (`/cadastro`) com um formulário feito em Vue (Composition API, `v-model` e validação sem bibliotecas externas).

## Tecnologias

- Node.js + npm
- [Nuxt 4](https://nuxt.com) (SSR)
- [Vue 3](https://vuejs.org) (`<script setup>`, Composition API)
- [Tailwind CSS 4](https://tailwindcss.com)
- [DaisyUI 5](https://daisyui.com)

## Como executar

Instale as dependências:

```bash
npm install
```

Inicie o servidor de desenvolvimento em `http://localhost:3000`:

```bash
npm run dev
```

## Rotas

| Rota | Arquivo | Descrição |
|---|---|---|
| `/` | `app/pages/index.vue` | Página inicial (hero do DaisyUI) com botões para `/example` e `/cadastro` |
| `/example` | `app/pages/example.vue` | Exemplo com o componente `mockup-window` |
| `/cadastro` | `app/pages/cadastro.vue` | Formulário de cadastro com validação |

## Formulário de cadastro

Campos: nome completo, e-mail, curso/área de atuação, semestre/período (1 a 10), interesses (checkboxes) e bio curta (até 200 caracteres).

- Nome, e-mail (com formato válido), curso e período são obrigatórios; os erros aparecem abaixo de cada campo.
- Ao enviar um formulário válido, os dados são exibidos no console do navegador, uma mensagem de sucesso é mostrada e o formulário é limpo.
- Não há backend: os dados não são salvos.
