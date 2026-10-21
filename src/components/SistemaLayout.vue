<script setup>
import { inject, ref } from 'vue'

const props = defineProps({
  title: { type: String, default: 'Sistema de Tutorías' },
  breadcrumb: { type: String, default: '' },
  user: { type: String, default: 'Nombre de usuario' },
  role: { type: String, default: 'Profesor/a' },
  showSidebar: { type: Boolean, default: true },
})

const navigateView = inject('navigateView', () => {})
const currentViewKey = inject('currentViewKey', ref('inicio'))

const navigation = [
  { title: 'General', items: [
    { key: 'inicio', label: 'Inicio', icon: '⌂' },
    { key: 'cursos', label: 'Cursos', icon: '▤' },
    { key: 'mis-tutorias', label: 'Mis tutorías', icon: '◷' },
    { key: 'notificaciones', label: 'Notificaciones', icon: '♧' },
  ] },
  { title: 'Tutorías', items: [
    { key: 'detalle-curso', label: 'Detalle de curso', icon: '▧' },
    { key: 'detalle-tutoria', label: 'Detalle de tutoría', icon: '▣' },
    { key: 'reservar-tutoria', label: 'Reservar tutoría', icon: '+' },
    { key: 'calificar-tutoria', label: 'Calificar tutoría', icon: '☆' },
  ] },
  { title: 'Mi cuenta', items: [
    { key: 'perfil', label: 'Mi perfil', icon: '◉' },
    { key: 'editar-perfil', label: 'Editar perfil', icon: '✎' },
    { key: 'cambiar-contrasena', label: 'Cambiar contraseña', icon: '⌑' },
  ] },
]
</script>

<template>
  <div class="app-shell">
    <header class="topbar">
      <button class="brand" type="button" @click="navigateView('inicio')">{{ title }}</button>
      <div class="account"><div class="account-copy"><span>{{ user }}</span><small>{{ role }}</small></div><button class="icon-btn" type="button" aria-label="Ver notificaciones" @click="navigateView('notificaciones')">♧</button><button class="avatar" type="button" aria-label="Ver perfil" @click="navigateView('perfil')">◉</button></div>
    </header>
    <nav v-if="!showSidebar" class="public-nav" aria-label="Navegación de acceso"><button type="button" @click="navigateView('inicio')">Inicio</button><button type="button" @click="navigateView('inicio-sesion')">Iniciar sesión</button><button class="public-primary" type="button" @click="navigateView('registrarse')">Crear cuenta</button></nav>
    <div class="workspace" :class="{ 'workspace-public': !showSidebar }">
      <aside v-if="showSidebar" class="sidebar" aria-label="Menú principal">
        <div v-for="section in navigation" :key="section.title" class="nav-section"><h2>{{ section.title }}</h2><button v-for="item in section.items" :key="item.key" class="nav-item" :class="{ active: currentViewKey === item.key }" type="button" :aria-current="currentViewKey === item.key ? 'page' : undefined" @click="navigateView(item.key)"><span class="nav-icon" aria-hidden="true">{{ item.icon }}</span><span>{{ item.label }}</span></button></div>
        <button class="session" type="button" @click="navigateView('cerrar-sesion')"><span aria-hidden="true">↪</span> Cerrar sesión</button>
      </aside>
      <main class="content"><div v-if="breadcrumb" class="breadcrumb">{{ breadcrumb }}</div><slot /></main>
    </div>
  </div>
</template>

<style>
:root { font-family: Inter, ui-sans-serif, system-ui, sans-serif; color: #253238; background: #f7f8fb; }
* { box-sizing: border-box; } button, input, select, textarea { font: inherit; } button { cursor: pointer; }
.app-shell { min-height: 100vh; background: #fafbfc; }.topbar { min-height: 76px; padding: 16px 28px; display:flex; align-items:center; justify-content:space-between; border-bottom:1px solid #d7dce2; background:#fff; }.brand { font-size:clamp(1.35rem,3vw,2rem); font-weight:800; letter-spacing:-.03em; }.account { display:flex; align-items:center; gap:12px; text-align:right; }.account span { font-weight:700; display:block; }.account small { display:block; color:#66727b; margin-left:auto; }.icon-btn,.avatar { border:0; background:transparent; font-size:1.35rem; }.avatar { font-size:1.8rem; }
.workspace { display:grid; grid-template-columns:235px 1fr; min-height:calc(100vh - 76px); }.sidebar { position:relative; border-right:1px solid #d7dce2; background:#fff; padding:20px 0; display:flex; flex-direction:column; }.sidebar h3 { margin:0 22px 10px; font-size:.95rem; text-transform:uppercase; letter-spacing:.08em; color:#68727a; }.course,.session { text-align:left; border:0; border-bottom:1px solid #e4e8ec; background:transparent; padding:14px 22px; font-weight:700; color:#3d4850; }.course.active { background:#e4ddf2; }.session { margin-top:auto; border-top:1px solid #e4e8ec; border-bottom:0; background:#e4ddf2; }
.content { padding:26px clamp(20px,4vw,56px); overflow:auto; }.breadcrumb { color:#65717a; font-size:.95rem; margin-bottom:18px; }.panel { background:#fff; border:1px solid #d9dfe4; border-radius:18px; padding:24px; box-shadow:0 8px 24px rgba(31,45,61,.05); }.panel h1,.panel h2 { margin:0 0 18px; }.muted { color:#6a757d; }.grid { display:grid; gap:18px; }.grid-2 { grid-template-columns:repeat(2,minmax(0,1fr)); }.grid-3 { grid-template-columns:repeat(3,minmax(0,1fr)); }.card { border:1px solid #d8dde2; border-radius:14px; overflow:hidden; background:#fff; }.card-head { height:76px; background:#70a0cc; }.card-head.red { background:#cc7b6f; }.card-body { padding:16px; }.card h3 { margin:0 0 6px; }.card p { margin:0 0 15px; color:#65717a; }
.actions { display:flex; gap:10px; flex-wrap:wrap; margin-top:20px; }.btn { border:1px solid #a9b4bc; border-radius:10px; padding:10px 16px; background:#fff; font-weight:700; }.btn.primary { background:#6b91c2; color:#fff; border-color:#6b91c2; }.btn.success { background:#b9d878; border-color:#9ebb5c; }.btn.danger { background:#dc8b80; border-color:#cf7166; }.btn.soft { background:#e7ddf2; border-color:#cdbde2; }
label { display:grid; gap:7px; font-weight:700; color:#40505a; } input,select,textarea { width:100%; border:1px solid #c8d0d6; border-radius:9px; padding:11px 12px; background:#fff; } textarea { min-height:100px; resize:vertical; }.form { max-width:760px; display:grid; gap:16px; }.form-row { display:grid; grid-template-columns:repeat(2,minmax(0,1fr)); gap:16px; }.notice { padding:14px 16px; border-radius:12px; background:#edf4d9; color:#4e6127; }.warning { background:#fff3d5; color:#795c1f; }.table { width:100%; border-collapse:collapse; }.table th,.table td { text-align:left; padding:13px 10px; border-bottom:1px solid #e1e5e8; }.table th { color:#68737b; font-size:.85rem; text-transform:uppercase; }.status { display:inline-flex; padding:5px 9px; border-radius:999px; background:#e4f0c9; color:#567026; font-size:.83rem; font-weight:700; }
@media (max-width:800px) { .workspace { grid-template-columns:1fr; }.sidebar { min-height:auto; }.session { margin-top:16px; }.grid-2,.grid-3,.form-row { grid-template-columns:1fr; }.topbar { align-items:flex-start; gap:12px; flex-direction:column; }.account { align-self:stretch; justify-content:flex-end; } }
</style>
<style>
.app-shell { background:#f4f6fa; }
.brand { border:0; background:transparent; padding:4px 0; color:#182e46; }
.account-copy span { color:#26384a; }
.account-copy small { margin-left:0; color:#7b8794; }
.public-nav { display:flex; justify-content:center; gap:12px; padding:14px 20px; background:#fff; border-bottom:1px solid #e3e8ef; }
.public-nav button { border:0; border-radius:10px; background:transparent; color:#36516b; padding:10px 16px; font-weight:700; }
.public-nav .public-primary { background:#285f91; color:#fff; }
.workspace-public { grid-template-columns:minmax(0,1fr); min-height:calc(100vh - 132px); }
.nav-section h2 { margin:0 10px 9px; font-size:.72rem; text-transform:uppercase; letter-spacing:.12em; color:#8995a2; }
.nav-item { width:100%; display:flex; align-items:center; gap:12px; text-align:left; border:0; border-radius:10px; background:transparent; padding:11px 12px; color:#506171; font-weight:650; }
.nav-item:hover { background:#f2f6fa; color:#285f91; }
.nav-item.active { background:#eaf2f9; color:#285f91; }
.nav-icon { width:22px; text-align:center; font-size:1.05rem; }
.session { display:flex; align-items:center; gap:10px; margin-top:auto; border:1px solid #f0d9d7; border-radius:10px; background:#fff7f6; color:#a34b44; padding:12px; font-weight:700; }
@media (max-width:800px) { .sidebar { display:grid; grid-template-columns:repeat(2,minmax(0,1fr)); gap:14px; border-right:0; border-bottom:1px solid #e3e8ef; }.session { grid-column:1/-1; margin-top:0; }.public-nav { flex-wrap:wrap; } }
@media (max-width:480px) { .sidebar { grid-template-columns:1fr; }.session { grid-column:auto; }.public-nav { justify-content:stretch; }.public-nav button { flex:1; } }
</style>
