<script setup>
import { inject } from 'vue'
import SistemaLayout from './SistemaLayout.vue'
const navigateView = inject('navigateView', () => {})
</script>
<template>
  <SistemaLayout breadcrumb="Espacio Curricular"><section class="panel"><div class="page-title"><div><h1>Cursos</h1><p class="muted">Elegí un espacio curricular para continuar.</p></div><button class="btn soft" @click="navigateView('agregar-curso')">＋ Agregar curso</button></div><div class="grid grid-3"><article class="card"><div class="card-head"></div><div class="card-body"><h3>Matemática</h3><p>5to año · 4° A</p><button class="btn primary" @click="navigateView('detalle-curso')">Ver curso</button></div></article><article class="card"><div class="card-head red"></div><div class="card-body"><h3>Borradores</h3><p>Sin tutorías publicadas</p><button class="btn" @click="navigateView('agregar-curso')">Editar curso</button></div></article><article class="card"><div class="card-head"></div><div class="card-body"><h3>Lengua</h3><p>3er año · 3° B</p><button class="btn primary" @click="navigateView('detalle-curso')">Ver curso</button></div></article></div></section></SistemaLayout>
</template>
<style scoped>.page-title{display:flex;align-items:center;justify-content:space-between;margin-bottom:22px}</style>




