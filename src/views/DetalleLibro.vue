<template>
  <div class="detalle-container" v-if="libroEncontrado">
    <router-link to="/libros" class="volver">← Volver al catálogo</router-link>
    
    <div class="detalle-card">
      <span class="badge">{{ libroEncontrado.categoria }}</span>
      <h2>{{ libroEncontrado.titulo }}</h2>
      <h4 class="autor">Escrito por: {{ libroEncontrado.autor }}</h4>
      
      <div class="descripcion">
        <p><strong>Descripción:</strong></p>
        <p>{{ libroEncontrado.descripcion || 'Este libro no tiene una descripción detallada.' }}</p>
      </div>
    </div>
  </div>
  
  <div v-else class="detalle-container error">
    <h2>Libro no encontrado</h2>
    <p>El identificador no corresponde a ningún libro en nuestro registro.</p>
    <router-link to="/libros" class="btn btn-primary" style="text-decoration: none; display: inline-block; margin-top: 1rem;">Volver</router-link>
  </div>
</template>

<script>
export default {
  props: ['libros'],
  computed: {
    libroEncontrado() {
      // Búsqueda del libro usando la ruta dinámica [cite: 28, 67]
      const id = parseInt(this.$route.params.id);
      return this.libros.find(l => l.id === id);
    }
  }
}
</script>

<style scoped>
.detalle-container {
  max-width: 600px;
  margin: 0 auto;
}
.volver {
  display: inline-block;
  margin-bottom: 1rem;
  color: var(--secondary);
  text-decoration: none;
  font-weight: 600;
}
.volver:hover { text-decoration: underline; }

.detalle-card {
  background: var(--surface);
  padding: 2.5rem;
  border-radius: 12px;
  box-shadow: 0 4px 15px rgba(0,0,0,0.05);
  border-top: 5px solid var(--primary);
}

.badge {
  display: inline-block;
  background: #e3f2fd;
  color: var(--secondary);
  font-size: 0.85rem;
  padding: 0.3rem 0.8rem;
  border-radius: 12px;
  font-weight: bold;
  margin-bottom: 1rem;
}

h2 { font-size: 2rem; color: var(--text-dark); margin-bottom: 0.5rem; }
.autor { color: var(--text-light); font-weight: normal; margin-bottom: 2rem; }

.descripcion {
  background: var(--bg-color);
  padding: 1.5rem;
  border-radius: 8px;
  line-height: 1.6;
}

.error { text-align: center; padding: 4rem 0; }
</style>