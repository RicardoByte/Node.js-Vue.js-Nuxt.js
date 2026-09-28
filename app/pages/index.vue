<script setup>
const areas = [
  { nome: 'Front-end', texto: 'Interfaces, componentes e tudo que aparece na tela.' },
  { nome: 'Back-end', texto: 'APIs, bancos de dados e a lógica por trás dos sistemas.' },
  { nome: 'Mobile', texto: 'Aplicativos para Android e iOS.' },
  { nome: 'UI/UX', texto: 'Pesquisa, protótipos e design centrado no usuário.' },
  { nome: 'Dados', texto: 'Análise, visualização e aprendizado de máquina.' },
  { nome: 'DevOps', texto: 'Deploy, automação e infraestrutura.' }
]
</script>

<template>
  <main class="home">
    <!-- Destaque principal -->
    <section class="hero">
      <div class="hero-conteudo">
        <h1>Aprenda, construa e cresça com quem programa junto.</h1>
        <p>
          Uma comunidade para estudantes de tecnologia trocarem experiência,
          montarem projetos reais e encontrarem sua área.
        </p>
        <div class="acoes">
          <NuxtLink to="/cadastro" class="btn btn-principal">Quero ser membro</NuxtLink>
          <a href="#areas" class="btn btn-secundario">Ver áreas</a>
        </div>
      </div>
    </section>

    <!-- Áreas -->
    <section id="areas" class="areas">
      <h2>Escolha por onde começar</h2>
      <p class="sub">No cadastro você marca quantas áreas quiser.</p>

      <ul class="lista">
        <li v-for="a in areas" :key="a.nome">
          <strong>{{ a.nome }}</strong>
          <span>{{ a.texto }}</span>
        </li>
      </ul>
    </section>

    <!-- Chamada final -->
    <section class="final">
      <h2>Leva menos de um minuto.</h2>
      <NuxtLink to="/cadastro" class="btn btn-principal">Preencher cadastro</NuxtLink>
    </section>
  </main>
</template>

<style scoped>
.home {
  --tinta: #14213d;
  --destaque: #ffc233;
  --papel: #f4f6f8;
  color: var(--tinta);
}

/* Hero */
.hero {
  background: var(--tinta);
  color: #fff;
  padding: 96px 24px;
}
.hero-conteudo {
  max-width: 760px;
  margin: 0 auto;
}
.hero h1 {
  font-size: clamp(2rem, 5vw, 3.5rem);
  line-height: 1.1;
  margin: 0 0 20px;
}
.hero p {
  font-size: 1.15rem;
  line-height: 1.6;
  max-width: 560px;
  margin: 0 0 32px;
  color: #d5dbe8;
}
.acoes {
  display: flex;
  flex-wrap: wrap;
  gap: 12px;
}

/* Botões */
.btn {
  display: inline-block;
  padding: 14px 24px;
  border-radius: 6px;
  font-weight: bold;
  text-decoration: none;
  transition: transform 0.15s;
}
.btn:hover {
  transform: translateY(-2px);
}
.btn:focus-visible {
  outline: 3px solid var(--destaque);
  outline-offset: 3px;
}
.btn-principal {
  background: var(--destaque);
  color: var(--tinta);
}
.btn-secundario {
  border: 2px solid #fff;
  color: #fff;
}

/* Áreas */
.areas {
  max-width: 760px;
  margin: 0 auto;
  padding: 72px 24px 24px;
}
.areas h2,
.final h2 {
  font-size: 1.8rem;
  margin: 0 0 8px;
}
.sub {
  margin: 0 0 32px;
  color: #4b5563;
}
.lista {
  list-style: none;
  margin: 0;
  padding: 0;
}
.lista li {
  display: grid;
  grid-template-columns: 140px 1fr;
  gap: 16px;
  padding: 18px 0;
  border-top: 1px solid #d1d5db;
}
.lista li:last-child {
  border-bottom: 1px solid #d1d5db;
}
.lista span {
  color: #4b5563;
  line-height: 1.5;
}

/* Chamada final */
.final {
  max-width: 760px;
  margin: 0 auto;
  padding: 56px 24px 96px;
}
.final h2 {
  margin-bottom: 20px;
}

/* Responsividade */
@media (max-width: 560px) {
  .hero {
    padding: 64px 20px;
  }
  .lista li {
    grid-template-columns: 1fr;
    gap: 4px;
  }
}

@media (prefers-reduced-motion: reduce) {
  .btn {
    transition: none;
  }
}
</style>
