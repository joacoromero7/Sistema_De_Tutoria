<script setup>
import { computed, inject, ref } from 'vue'
import SistemaLayout from './SistemaLayout.vue'

const navigateView = inject('navigateView', () => {})
const reserved = ref(false)
const selectedDate = ref('')
const currentMonth = ref(new Date(new Date().getFullYear(), new Date().getMonth(), 1))
const weekdays = ['Lun', 'Mar', 'Mié', 'Jue', 'Vie', 'Sáb', 'Dom']
const monthNames = ['Enero', 'Febrero', 'Marzo', 'Abril', 'Mayo', 'Junio', 'Julio', 'Agosto', 'Septiembre', 'Octubre', 'Noviembre', 'Diciembre']
const currentYear = new Date().getFullYear()
const years = Array.from({ length: 11 }, (_, index) => currentYear - 5 + index)
const holidays = {
  '2026-01-01': 'Año Nuevo', '2026-02-16': 'Carnaval', '2026-02-17': 'Carnaval', '2026-03-24': 'Día Nacional de la Memoria por la Verdad y la Justicia',
  '2026-04-02': 'Día del Veterano y de los Caídos en la Guerra de Malvinas', '2026-04-03': 'Viernes Santo', '2026-05-01': 'Día del Trabajador',
  '2026-05-25': 'Día de la Revolución de Mayo', '2026-06-15': 'Paso a la Inmortalidad del Gral. Martín Miguel de Güemes', '2026-06-20': 'Paso a la Inmortalidad del Gral. Manuel Belgrano',
  '2026-07-09': 'Día de la Independencia', '2026-08-17': 'Paso a la Inmortalidad del Gral. José de San Martín', '2026-10-12': 'Día del Respeto a la Diversidad Cultural',
  '2026-11-09': 'Feriado nacional especial', '2026-11-20': 'Día de la Soberanía Nacional', '2026-12-08': 'Inmaculada Concepción de María', '2026-12-25': 'Navidad',
}

const monthLabel = computed(() => `${monthNames[currentMonth.value.getMonth()]} ${currentMonth.value.getFullYear()}`)
const calendarDays = computed(() => {
  const month = currentMonth.value
  const first = new Date(month.getFullYear(), month.getMonth(), 1)
  const start = (first.getDay() + 6) % 7
  const daysInMonth = new Date(month.getFullYear(), month.getMonth() + 1, 0).getDate()
  return Array.from({ length: 42 }, (_, index) => {
    const number = index - start + 1
    const date = number > 0 && number <= daysInMonth ? new Date(month.getFullYear(), month.getMonth(), number) : null
    const key = dateKey(date)
    return { number, date, holiday: date ? holidays[key] : '', past: date ? key < todayKey() : false }
  })
})

function dateKey(date) {
  if (!date) return ''
  return `${date.getFullYear()}-${String(date.getMonth() + 1).padStart(2, '0')}-${String(date.getDate()).padStart(2, '0')}`
}
function todayKey() { return dateKey(new Date()) }
function chooseDate(date) {
  if (!date || holidays[dateKey(date)] || dateKey(date) < todayKey()) return
  selectedDate.value = dateKey(date)
}
function shiftMonth(amount) { currentMonth.value = new Date(currentMonth.value.getFullYear(), currentMonth.value.getMonth() + amount, 1) }
function selectMonth(event) { currentMonth.value = new Date(currentMonth.value.getFullYear(), Number(event.target.value), 1) }
function selectYear(event) { currentMonth.value = new Date(Number(event.target.value), currentMonth.value.getMonth(), 1) }
function reserve() { reserved.value = true }
</script>

<template>
  <SistemaLayout breadcrumb="Espacio Curricular > Matemática > Reservar tutoría">
    <section class="panel reservation-panel"><div class="reservation-heading"><div><span class="eyebrow">Nueva solicitud</span><h1>Reservar tutoría</h1><p class="muted">Elegí una fecha y horario para solicitar tu espacio.</p></div><span class="step-badge">Paso 1 de 2</span></div>
      <form class="form reservation-form" @submit.prevent="reserve"><div class="form-row"><label>Estudiante<input value="Juan Pérez" /></label><label>Curso<select><option>5to año · 4° A</option><option>3er año · 3° B</option></select></label></div><div class="form-row"><label>Materia<input value="Matemática" /></label><label>Docente<select><option>María Becerra</option><option>Joaquín Pérez</option></select></label></div>
        <div class="date-picker-wrap"><label>Fecha de la tutoría</label><div class="calendar-card"><div class="calendar-toolbar"><button type="button" class="calendar-arrow" aria-label="Mes anterior" @click="shiftMonth(-1)">‹</button><select class="calendar-select month-select" :value="currentMonth.getMonth()" aria-label="Seleccionar mes" @change="selectMonth"><option v-for="(month, index) in monthNames" :key="month" :value="index">{{ month }}</option></select><select class="calendar-select year-select" :value="currentMonth.getFullYear()" aria-label="Seleccionar año" @change="selectYear"><option v-for="year in years" :key="year" :value="year">{{ year }}</option></select><button type="button" class="calendar-arrow" aria-label="Mes siguiente" @click="shiftMonth(1)">›</button></div><div class="calendar-weekdays"><span v-for="day in weekdays" :key="day">{{ day }}</span></div><div class="calendar-grid"><button v-for="(day, index) in calendarDays" :key="index" type="button" class="calendar-day" :class="{ empty: !day.date, holiday: day.holiday, past: day.past, selected: selectedDate === dateKey(day.date) }" :title="day.holiday || (day.past ? 'Fecha pasada' : '')" :disabled="!day.date || day.holiday || day.past" @click="chooseDate(day.date)">{{ day.date ? day.number : '' }}</button></div><div class="calendar-legend"><span><i class="legend-dot holiday-dot"></i> Feriado</span><span><i class="legend-dot past-dot"></i> Fecha pasada</span><span><i class="legend-dot selected-dot"></i> Fecha elegida</span></div></div><p class="selected-date">{{ selectedDate ? `Fecha seleccionada: ${new Date(`${selectedDate}T12:00:00`).toLocaleDateString('es-AR', { weekday: 'long', day: 'numeric', month: 'long' })}` : 'Seleccioná un día disponible en el calendario.' }}</p></div>
        <label>Horario<select><option>Miércoles · 7:30 a 8:20</option><option>Jueves · 15:30 a 16:30</option></select></label><label>Motivo<textarea placeholder="Recuperación de contenidos"></textarea></label><button class="btn primary" :disabled="!selectedDate">Confirmar reserva</button><div v-if="reserved" class="notice">Solicitud registrada y pendiente de confirmación. <button type="button" class="btn soft" @click="navigateView('mis-tutorias')">Ver mis tutorías</button></div>
      </form>
    </section>
  </SistemaLayout>
</template>

<style scoped>
.reservation-heading{display:flex;align-items:flex-start;justify-content:space-between;gap:20px;margin-bottom:24px}.eyebrow{color:#315fce;font-size:.78rem;font-weight:800;letter-spacing:.12em;text-transform:uppercase}.reservation-heading h1{margin:7px 0 8px}.step-badge{padding:8px 12px;border-radius:999px;background:#edf3ff;color:#315fce;font-size:.8rem;font-weight:800;white-space:nowrap}.date-picker-wrap{display:grid;gap:9px}.calendar-card{max-width:450px;padding:18px;border:1px solid #e1e8f3;border-radius:18px;background:#fbfcff;box-shadow:0 10px 26px rgba(36,75,168,.06)}.calendar-toolbar{display:flex;align-items:center;justify-content:space-between;gap:6px;margin-bottom:16px;color:#17233c}.calendar-select{border:1px solid #dce4ef;border-radius:8px;padding:7px 8px;background:#fff;color:#17233c;font-weight:750}.month-select{min-width:112px}.year-select{min-width:76px}.calendar-arrow{width:32px;height:32px;border:0;border-radius:9px;background:#edf3ff;color:#315fce;font-size:1.5rem;line-height:1}.calendar-weekdays,.calendar-grid{display:grid;grid-template-columns:repeat(7,1fr);gap:5px}.calendar-weekdays{margin-bottom:6px;color:#9aa8bc;font-size:.72rem;font-weight:800;text-align:center}.calendar-day{aspect-ratio:1;border:0;border-radius:9px;background:transparent;color:#53627a}.calendar-day:not(:disabled):hover{background:#e8efff;color:#315fce}.calendar-day.empty{pointer-events:none}.calendar-day.past{background:#eef1f5;color:#b5bdc9;text-decoration:line-through;cursor:not-allowed}.calendar-day.holiday{background:#fff0ef;color:#c05a54;text-decoration:line-through;cursor:not-allowed}.calendar-day.selected{background:#315fce;color:#fff;font-weight:800;box-shadow:0 5px 12px rgba(49,95,206,.25)}.calendar-legend{display:flex;gap:12px;flex-wrap:wrap;margin-top:14px;color:#7c8aa0;font-size:.72rem}.calendar-legend span{display:inline-flex;align-items:center;gap:5px}.legend-dot{width:8px;height:8px;border-radius:50%;display:inline-block}.holiday-dot{background:#e98982}.past-dot{background:#b5bdc9}.selected-dot{background:#315fce}.selected-date{color:#315fce;font-size:.9rem;font-weight:700}.reservation-form>.btn:disabled{opacity:.45;cursor:not-allowed}.reservation-panel{max-width:920px}@media(max-width:600px){.reservation-heading{flex-direction:column}.calendar-card{max-width:none}.calendar-toolbar{flex-wrap:wrap}.calendar-select{flex:1}}
</style>
