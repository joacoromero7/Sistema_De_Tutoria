<script setup>
import SistemaLayout from './SistemaLayout.vue'
import { ref } from 'vue'; const sent=ref(false); const rating=ref(0)
</script>
<template><SistemaLayout breadcrumb="Mis tutorías > Calificar"><section class="panel"><h1>Calificar tutoría</h1><p class="muted">Contanos cómo fue la tutoría con María Becerra.</p><form class="form" @submit.prevent="sent=true"><label>Valoración<div class="stars"><button v-for="n in 5" :key="n" type="button" @click="rating=n">{{ n <= rating ? '★' : '☆' }}</button></div></label><label>Comentario<textarea placeholder="Escribí una opinión"></textarea></label><button class="btn primary">Enviar calificación</button><p v-if="sent" class="notice">Gracias por tu valoración.</p></form></section></SistemaLayout></template>
<style scoped>.stars{display:flex;gap:8px}.stars button{border:0;background:transparent;color:#e4ad36;font-size:2rem;padding:0}</style>
