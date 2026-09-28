<template>
  <div>
    <nav class="menu">
      <NuxtLink to="/">Início</NuxtLink>
      <NuxtLink to="/cadastro">Cadastro</NuxtLink>
    </nav>

    <NuxtPage />
  </div>
</template>

<style>
body {
  margin: 0;
  font-family: Arial, sans-serif;
  background: #f4f6f8;
}
.menu {
  display: flex;
  gap: 16px;
  padding: 16px 24px;
  background: #1f2937;
}
.menu a {
  color: #fff;
  text-decoration: none;
}
.menu a.router-link-active {
  font-weight: bold;
  text-decoration: underline;
}
</style>