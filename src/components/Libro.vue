<template>
  <div class="libro-card">
    <div class="libro-info">
      <span class="badge">{{ libro.categoria }}</span>
      <h3>{{ libro.titulo }}</h3>
      <p class="autor">{{ libro.autor }}</p>
    </div>
    <div class="libro-acciones">
      <router-link :to="`/libros/${libro.id}`" class="btn btn-outline btn-sm">Ver Detalle</router-link>
      <button @click="$emit('eliminar')" class="btn btn-danger btn-sm">Eliminar</button>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    libro: Object // Uso de props y directivas de binding implícitas 
  }
}
</script>

<style scoped>
.libro-card {
  border: 1px solid var(--border);
  border-radius: 8px;
  padding: 1.2rem;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  transition: transform 0.2s, box-shadow 0.2s;
  background: white;
}
.libro-card:hover {
  transform: translateY(-3px);
  box-shadow: 0 6px 12px rgba(0,0,0,0.08);
}

.badge {
  display: inline-block;
  background: #e3f2fd;
  color: var(--secondary);
  font-size: 0.75rem;
  padding: 0.2rem 0.5rem;
  border-radius: 12px;
  font-weight: bold;
  margin-bottom: 0.5rem;
}

h3 { font-size: 1.1rem; color: var(--text-dark); margin-bottom: 0.25rem; }
.autor { color: var(--text-light); font-size: 0.9rem; margin-bottom: 1rem; }

.libro-acciones {
  display: flex;
  gap: 0.5rem;
}
.btn-sm { padding: 0.4rem 0.8rem; font-size: 0.85rem; text-decoration: none; text-align: center; flex: 1;}
</style>