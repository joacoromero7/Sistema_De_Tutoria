<script setup>
import { inject, ref } from 'vue'
import SistemaLayout from './SistemaLayout.vue'
const navigateView = inject('navigateView', () => {})
const closed = ref(false)
</script>
<template><SistemaLayout :show-sidebar="false"><section class="panel auth"><h1>{{ closed ? 'Sesión cerrada' : 'Cerrar sesión' }}</h1><p class="muted">{{ closed ? 'Podés volver a iniciar sesión cuando quieras.' : '¿Querés salir del Sistema de Tutorías?' }}</p><div class="actions"><button v-if="!closed" class="btn danger" @click="closed=true">Cerrar sesión</button><button class="btn primary" @click="navigateView('inicio-sesion')">Ir a iniciar sesión</button></div></section></SistemaLayout></template>
<style scoped>.auth{max-width:540px;margin:7vh auto}</style>
