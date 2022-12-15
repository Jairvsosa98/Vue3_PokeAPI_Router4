<script setup>
  const hoy = new Date();
  const opciones = { weekday: 'long', year: 'numeric', month: 'short', day: 'numeric' };

  const fechaActual = hoy.toLocaleDateString('es-PE', opciones)
</script>

<template>
  <div class="card text-center bg-dark">
    <div class="card-header">
      Vue Router + Vite + PokeAPI
    </div>
    <div class="card-body">
      <h5 class="card-title">Proyecto desarrollado con Vue3</h5>
      <p class="card-text">Este proyecto ha sido desarrollado con la finalidad de aprender más sobre vue Router v4.</p>
      <a href="#" class="btn btn-primary">Ver Pokemon</a>
    </div>
    <div class="card-footer text-muted">
      {{fechaActual}}
    </div>
  </div>
</template>
