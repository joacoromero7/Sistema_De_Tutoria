<script setup>
import { inject } from 'vue'
import SistemaLayout from './SistemaLayout.vue'
const navigateView = inject('navigateView', () => {})
</script>

<template>
  <SistemaLayout breadcrumb="Inicio">
    <section class="panel"><h1>Bienvenido/a al Sistema de Tutorías</h1><p class="muted">Accedé rápidamente a tus cursos, tutorías y notificaciones.</p><div class="grid grid-3">
      <article class="card"><div class="card-head"></div><div class="card-body"><h3>Cursos</h3><p>Consultá materias y espacios curriculares.</p><button class="btn primary" @click="navigateView('cursos')">Ver cursos</button></div></article>
      <article class="card"><div class="card-head red"></div><div class="card-body"><h3>Mis tutorías</h3><p>Revisá reservas y estados.</p><button class="btn soft" @click="navigateView('mis-tutorias')">Ver tutorías</button></div></article>
      <article class="card"><div class="card-body"><h3>Calendario general</h3><p>Próximas actividades y horarios.</p><button class="btn success" @click="navigateView('notificaciones')">Abrir calendario</button></div></article>
    </div></section>
  </SistemaLayout>
</template>
