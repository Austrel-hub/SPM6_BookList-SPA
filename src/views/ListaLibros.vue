<template>
  <div class="catalogo-grid">
    <aside class="panel-formulario">
      <h2>Añadir Nuevo Libro</h2>
      
      <form @submit.prevent="submitForm" class="form">
        <div class="form-group">
          <label>Título</label>
          <input type="text" v-model="nuevoLibro.titulo" @keyup.enter="submitForm" required placeholder="Ej: Cien años de soledad">
        </div>
        
        <div class="form-group">
          <label>Autor</label>
          <input type="text" v-model="nuevoLibro.autor" required placeholder="Ej: Gabriel García Márquez">
        </div>
        
        <div class="form-group">
          <label>Categoría</label>
          <select v-model="nuevoLibro.categoria">
            <option value="Ficción">Ficción</option>
            <option value="Tecnología">Tecnología</option>
            <option value="Ciencias">Ciencias</option>
            <option value="Historia">Historia</option>
          </select>
        </div>
        
        <div class="form-group">
          <label>Descripción</label>
          <textarea v-model="nuevoLibro.descripcion" rows="3" placeholder="Breve sinopsis..."></textarea>
        </div>
        
        <button type="submit" class="btn btn-primary w-100">Guardar Libro</button>
      </form>

      <div class="preview-card" v-show="nuevoLibro.titulo || nuevoLibro.autor">
        <h4>👀 Previsualización</h4>
        <p><strong>{{ nuevoLibro.titulo || 'Sin título' }}</strong></p>
        <p class="text-sm">{{ nuevoLibro.autor || 'Sin autor' }} - <em>{{ nuevoLibro.categoria }}</em></p>
      </div>
    </aside>

    <section class="panel-lista">
      <h2>Catálogo Actual ({{ libros.length }})</h2>
      
      <div v-if="libros.length === 0" class="empty-state">
        <p>No hay libros registrados. Añade uno desde el formulario.</p>
      </div>
      
      <div v-else class="lista-libros">
        <Libro 
          v-for="libro in libros" 
          :key="libro.id" 
          :libro="libro" 
          @eliminar="$emit('eliminar', libro.id)" 
        />
      </div>
    </section>
  </div>
</template>

<script>
import Libro from '../components/Libro.vue'

export default {
  components: { Libro },
  props: ['libros'], // Recibe los libros de App.vue [cite: 67]
  data() {
    return {
      nuevoLibro: { titulo: '', autor: '', categoria: 'Ficción', descripcion: '' }
    }
  },
  methods: {
    submitForm() {
      if (this.nuevoLibro.titulo && this.nuevoLibro.autor) {
        this.$emit('agregar', this.nuevoLibro);
        // Resetear formulario
        this.nuevoLibro = { titulo: '', autor: '', categoria: 'Ficción', descripcion: '' };
      }
    }
  }
}
</script>

<style scoped>
.catalogo-grid {
  display: grid;
  grid-template-columns: 1fr 2fr;
  gap: 2rem;
}

.panel-formulario, .panel-lista {
  background: var(--surface);
  padding: 1.5rem;
  border-radius: 12px;
  box-shadow: 0 4px 6px rgba(0,0,0,0.05);
}

h2 { margin-bottom: 1.5rem; color: var(--secondary); font-size: 1.3rem; }

.form-group { margin-bottom: 1rem; }
label { display: block; margin-bottom: 0.5rem; font-weight: 600; font-size: 0.9rem; }
input, select, textarea {
  width: 100%;
  padding: 0.75rem;
  border: 1px solid var(--border);
  border-radius: 6px;
  font-family: inherit;
  transition: border-color 0.3s;
}
input:focus, select:focus, textarea:focus {
  outline: none;
  border-color: var(--primary);
}

.w-100 { width: 100%; margin-top: 1rem; }

.preview-card {
  margin-top: 1.5rem;
  padding: 1rem;
  background-color: #e8f5e9;
  border-left: 4px solid var(--primary);
  border-radius: 4px;
}
.text-sm { font-size: 0.85rem; color: var(--text-light); }

.empty-state {
  text-align: center;
  padding: 3rem;
  color: var(--text-light);
  background: var(--bg-color);
  border-radius: 8px;
  border: 2px dashed var(--border);
}

.lista-libros {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
  gap: 1rem;
}
</style>