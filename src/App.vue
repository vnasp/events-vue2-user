<template>
  <div id="app">
      <!-- El e.preventDefault() de Vue2 -->
    <form @submit.prevent="send">
      <div class="form__inputs">
        <div class="form__input">
          <label :style="changeLabelColor(nuevaCita.paciente)" for="paciente">Paciente</label>
          <input id="paciente" type="text" v-model="nuevaCita.paciente" @input="validateAppointment" />
        </div>
        <div class="form__input">
          <label :style="changeLabelColor(nuevaCita.fecha)" for="fecha">Fecha</label>
          <input id="fecha" type="date" v-model="nuevaCita.fecha" @input="validateAppointment" />
        </div>
        <div class="form__input">
          <label :style="changeLabelColor(nuevaCita.hora)" for="hora">Hora</label>
          <input id="hora" type="time" v-model="nuevaCita.hora" @input="validateAppointment" />
        </div>
        <div class="form__input">
          <label :style="changeLabelColor(nuevaCita.gravedadSeleccionada)" for="gravedad">Gravedad</label>
          <select id="gravedad" v-model="nuevaCita.gravedadSeleccionada" @change="validateAppointment">
            <option v-for="(nivel, index) in gravedad" :key="index" :value="nivel">{{ nivel }}</option>
          </select>
        </div>
        <div class="form__input">
          <label :style="changeLabelColor(nuevaCita.motivo)" for="motivo">Motivo</label>
          <input id="motivo" type="text" v-model="nuevaCita.motivo" @input="validateAppointment" />
        </div>
      </div>
      <button :disabled="!isFormValid" @click="addAppointment">Agregar</button>
    </form>
    <!-- Se evalúa el largo del array -->
    <div v-if="citas.length === 0">
      <p>Aún no hay consultas registradas.</p>
    </div>
    <!-- Se mapean las citas con un v-for -->
    <div v-else class="appointments">
      <AppointmentsList
        v-for="(cita, index) in citas"
        :key="index"
        :cita="cita"
        @deleteAppointment="citas.splice(index, 1)"
      />
    </div>
  </div>
</template>

<script>
import AppointmentsList from "./components/AppointmentsList.vue"

export default {
  name: 'App',
  components: {
    AppointmentsList,
  },
  data: () => ({
    nuevaCita: {
      paciente: '',
      fecha: '',
      hora: '',
      gravedadSeleccionada: '',
      motivo: ''
    },
    citas: [],
    gravedad: ['Baja', 'Media', 'Alta'],
    isFormValid: false
  }),
  methods: {
    send() {
      console.log("Enviando...");
    },
    changeLabelColor(value) {
      return {
        color: value ? 'black' : 'red'
      };
    },
    validateAppointment() {
      this.isFormValid = this.nuevaCita.paciente && this.nuevaCita.fecha && this.nuevaCita.hora && this.nuevaCita.gravedadSeleccionada && this.nuevaCita.motivo;
    },
    addAppointment() {
      const nuevaCita = { ...this.nuevaCita };
      this.citas.push(nuevaCita);
      this.nuevaCita = {
        paciente: '',
        fecha: '',
        hora: '',
        gravedadSeleccionada: '',
        motivo: ''
      };
      this.validateAppointment();
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  padding-top: 60px;
  width: 50%;
  margin: auto;
}

form {
  padding: 1rem;
  border: 1px solid gray;
}

label {
  font-weight: 700;
}

.form__inputs {
  display: flex;
  flex-direction: row;
  justify-content: space-around;
}

.form__input {
  display: flex;
  flex-direction: column;
}

.appointments{
  display:flex;
  flex-direction: row;
  justify-content: space-around;
}
</style>
