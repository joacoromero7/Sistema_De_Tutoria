<script setup>
import { provide, ref, shallowRef } from 'vue'
import CalificarTutoria from './components/CalificarTutoria.vue'
import CambiarContrasena from './components/CambiarContrasena.vue'
import CerrarSesion from './components/CerrarSesion.vue'
import Cursos from './components/Cursos.vue'
import DetalleCurso from './components/DetalleCurso.vue'
import DetalleTutoria from './components/DetalleTutoria.vue'
import EditarPerfil from './components/EditarPerfil.vue'
import Home from './components/Home.vue'
import InicioSesion from './components/InicioSesion.vue'
import MisTutorias from './components/MisTutorias.vue'
import Notificaciones from './components/Notificaciones.vue'
import Perfil from './components/Perfil.vue'
import RecuperarContrasena from './components/RecuperarContrasena.vue'
import Registrarse from './components/Registrarse.vue'
import ReservarTutoria from './components/ReservarTutoria.vue'

const views = {
  inicio: Home,
  cursos: Cursos,
  'mis-tutorias': MisTutorias,
  'detalle-curso': DetalleCurso,
  'detalle-tutoria': DetalleTutoria,
  'reservar-tutoria': ReservarTutoria,
  'calificar-tutoria': CalificarTutoria,
  perfil: Perfil,
  'editar-perfil': EditarPerfil,
  notificaciones: Notificaciones,
  'cambiar-contrasena': CambiarContrasena,
  'inicio-sesion': InicioSesion,
  registrarse: Registrarse,
  'recuperar-contrasena': RecuperarContrasena,
  'cerrar-sesion': CerrarSesion,
}

const activeView = shallowRef(Home)
const activeViewKey = ref('inicio')

provide('navigateView', (viewKey) => {
  if (!views[viewKey]) return
  activeViewKey.value = viewKey
  activeView.value = views[viewKey]
  window.scrollTo({ top: 0, behavior: 'smooth' })
})
provide('currentViewKey', activeViewKey)
</script>

<template>
  <component :is="activeView" :key="activeViewKey" />
</template>
