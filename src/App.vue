<template>
  <div id="app">
    <header class="navbar">
      <div class="nav-brand">📚 Editorial Nova</div>
      <nav>
        <router-link to="/" class="nav-link">Inicio</router-link>
        <router-link to="/libros" class="nav-link">Catálogo</router-link>
      </nav>
      <div class="user-info">
        <span>Hola, {{ nombreUsuario }}</span>
        <button @click.once="saludar" class="btn btn-outline">👋 Saludar (1 vez)</button>
      </div>
    </header>

    <main class="container">
      <router-view 
        :libros="libros" 
        @agregar="agregarLibro" 
        @eliminar="eliminarLibro"
      />
    </main>
  </div>
</template>

<script>
export default {
  data() {
    return {
      nombreUsuario: 'Admin',
      libros: [] // Estado centralizado [cite: 26]
    }
  },
  methods: {
    saludar() {
      alert('¡Bienvenido al sistema de gestión!');
    },
    agregarLibro(nuevoLibro) {
      this.libros.push({ ...nuevoLibro, id: Date.now() });
    },
    eliminarLibro(id) {
      this.libros = this.libros.filter(l => l.id !== id);
    }
  }
}
</script>

<style>
/* --- PALETA DE COLORES Y ESTILOS GLOBALES --- */
:root {
  --primary: #2e7d32; /* Verde profesional */
  --primary-hover: #1b5e20;
  --secondary: #1565c0; /* Azul profundo */
  --bg-color: #f4f6f8;
  --surface: #ffffff;
  --text-dark: #333333;
  --text-light: #666666;
  --danger: #d32f2f;
  --border: #e0e0e0;
}

* { box-sizing: border-box; margin: 0; padding: 0; }

body {
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  background-color: var(--bg-color);
  color: var(--text-dark);
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 2rem;
}

/* NAVBAR */
.navbar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  background-color: var(--surface);
  padding: 1rem 2rem;
  box-shadow: 0 2px 4px rgba(0,0,0,0.05);
}

.nav-brand { font-size: 1.5rem; font-weight: bold; color: var(--secondary); }

.nav-link {
  text-decoration: none;
  color: var(--text-light);
  font-weight: 600;
  margin: 0 1rem;
  padding-bottom: 0.25rem;
  transition: color 0.3s;
}
.nav-link:hover, .router-link-active {
  color: var(--primary);
  border-bottom: 2px solid var(--primary);
}

.user-info { display: flex; align-items: center; gap: 1rem; font-weight: 500;}

/* BOTONES */
.btn {
  padding: 0.6rem 1.2rem;
  border: none;
  border-radius: 6px;
  cursor: pointer;
  font-weight: 600;
  transition: all 0.3s ease;
}
.btn-primary { background-color: var(--primary); color: white; }
.btn-primary:hover { background-color: var(--primary-hover); }
.btn-danger { background-color: var(--danger); color: white; }
.btn-outline { background-color: transparent; border: 1px solid var(--secondary); color: var(--secondary); }
.btn-outline:hover { background-color: var(--secondary); color: white; }
</style>