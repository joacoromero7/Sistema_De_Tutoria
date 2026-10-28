<script setup>
import { inject, ref } from 'vue'
import SistemaLayout from './SistemaLayout.vue'
const navigateView = inject('navigateView', () => {})
const message = ref('')
function showMessage(text) { message.value = text }
</script>
<template><SistemaLayout breadcrumb="Espacio Curricular > Matemática > Detalles"><section class="panel"><h1>Detalle de tutoría</h1><div class="grid grid-2"><div><p><b>Citación:</b> #T-2026-0847</p><p><b>Fecha de creación:</b> 05/08/2026 · 09:12</p><p><b>Curso:</b> 5to año</p><p><b>Materia:</b> Matemática</p><p><b>Docente:</b> María Becerra</p><p><b>Estudiante:</b> Juan Pérez</p></div><div><p><b>Día y horario:</b> Miércoles 12/08 · 7:30 a 8:20</p><p><b>Lugar:</b> Aula 4</p><p><b>Motivo:</b> Recuperación de contenidos</p><p><b>Estado:</b> <span class="status">Confirmada</span></p><p><b>WhatsApp:</b> Enviado</p><p><b>Gmail:</b> Enviado</p></div></div><div class="actions"><button class="btn primary" @click="showMessage('La edición de la tutoría está lista para conectar con la API.')">Editar</button><button class="btn soft" @click="navigateView('reservar-tutoria')">Reprogramar</button><button class="btn danger" @click="showMessage('La tutoría fue marcada para cancelar.')">Cancelar</button><button class="btn success" @click="showMessage('La notificación fue enviada.')">Enviar</button></div><p v-if="message" class="notice">{{ message }}</p></section></SistemaLayout></template>




