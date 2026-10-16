<script setup>
import SistemaLayout from './SistemaLayout.vue'
import { ref } from 'vue'; const notifications=ref([{title:'Tutoría confirmada',body:'Matemática · Miércoles 12/08 · 7:30',date:'Hoy',read:false},{title:'Nueva tutoría disponible',body:'Se publicó un espacio de recuperación para 5to año.',date:'Ayer',read:true}]); function mark(n){n.read=true}
</script>
<template><SistemaLayout breadcrumb="Notificaciones"><section class="panel"><h1>Notificaciones</h1><div v-for="n in notifications" :key="n.title" class="notification" :class="{read:n.read}" @click="mark(n)"><div><b>{{ n.title }}</b><p>{{ n.body }}</p></div><small>{{ n.date }}</small></div></section></SistemaLayout></template>
<style scoped>.notification{display:flex;justify-content:space-between;gap:16px;padding:18px 0;border-bottom:1px solid #e1e5e8}.notification p{margin:6px 0 0;color:#64717a}.notification:not(.read){border-left:4px solid #b9d878;padding-left:14px}.notification small{color:#78838b;white-space:nowrap}</style>
