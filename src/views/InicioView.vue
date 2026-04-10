<template>
  <div class="hero">
    <h1>Gestión Inteligente de Catálogo</h1>
    <p>Administra los libros de Editorial Nova de forma rápida, eficiente y centralizada.</p>
    <router-link to="/libros" class="btn btn-primary" style="display: inline-block; margin-top: 1rem; text-decoration: none;">
      Ir al Catálogo
    </router-link>
  </div>
</template>

<style scoped>
.hero {
  text-align: center;
  padding: 4rem 2rem;
  background-color: var(--surface);
  border-radius: 12px;
  box-shadow: 0 4px 6px rgba(0,0,0,0.05);
  margin-top: 2rem;
}
.hero h1 { color: var(--secondary); margin-bottom: 1rem; font-size: 2.5rem; }
.hero p { color: var(--text-light); font-size: 1.2rem; }
</style>