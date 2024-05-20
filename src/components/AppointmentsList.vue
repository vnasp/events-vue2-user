<template> 
<!-- Se asigna el color con un operador ternario -->
  <div class="card"
    :style="{ backgroundColor: cita.gravedadSeleccionada === 'Baja' ? 'green' : cita.gravedadSeleccionada === 'Media' ? 'yellow' : 'red'}">
    <p><strong>Paciente:</strong> {{ cita.paciente }}</p>
    <p><strong>Fecha:</strong> {{ cita.fecha }}</p>
    <p><strong>Hora:</strong> {{ cita.hora }}</p>
    <p><strong>Gravedad:</strong> {{ cita.gravedadSeleccionada }}</p>
    <p><strong>Motivo:</strong> {{ cita.motivo }}</p>
    <!-- Con $emit se pasa de hijo a padre -->
    <button @click="$emit('deleteAppointment')">Eliminar</button>
  </div>
</template>

<script>
export default {
  name: 'AppointmentsList',
  props: {
    cita: {
      type: Object,
      required: true
    }
  }
}
</script>

<style>
.card {
  border-radius: 1rem;
  padding: 1rem;
  color: black;
}
</style>
