<template>
  <div class="form-container">
    <h2>Registro de Usuario</h2>
    <form @submit.prevent="validarFormulario">
      <!-- Campo Nombre -->
      <div>
        <label for="nombre">Nombre:</label>
        <input type="text" v-model="form.nombre" id="nombre" />
        <span class="error" v-if="errores.nombre">{{ errores.nombre }}</span>
      </div>

      <!-- Campo Dirección -->
      <div>
        <label for="direccion">Dirección:</label>
        <input type="text" v-model="form.direccion" id="direccion" />
        <span class="error" v-if="errores.direccion">{{ errores.direccion }}</span>
      </div>

      <!-- Campo Edad -->
      <div>
        <label for="edad">Edad:</label>
        <input type="number" v-model="form.edad" id="edad" />
        <span class="error" v-if="errores.edad">{{ errores.edad }}</span>
      </div>

      <button type="submit">Registrar</button>
    </form>

    <!-- Resultado -->
    <div v-if="registroExitoso" class="success">
      <p>✅ Registro exitoso:</p>
      <pre>{{ form }}</pre>
    </div>
  </div>
</template>

<script>
export default {
  name: "Formulario",
  data() {
    return {
      form: {
        nombre: "",
        direccion: "",
        edad: ""
      },
      errores: {},
      registroExitoso: false
    };
  },
  methods: {
    validarFormulario() {
      this.errores = {};
      this.registroExitoso = false;

      // Validación Nombre
      if (!this.form.nombre) {
        this.errores.nombre = "El nombre es obligatorio.";
      } else if (!/^[a-zA-Z\s]+$/.test(this.form.nombre)) {
        this.errores.nombre = "El nombre solo puede contener letras.";
      }

      // Validación Dirección
      if (!this.form.direccion) {
        this.errores.direccion = "La dirección es obligatoria.";
      }

      // Validación Edad
      if (!this.form.edad) {
        this.errores.edad = "La edad es obligatoria.";
      } else if (this.form.edad <= 0 || this.form.edad > 120) {
        this.errores.edad = "La edad no es válida.";
      }

      // Si no hay errores -> éxito
      if (Object.keys(this.errores).length === 0) {
        this.registroExitoso = true;
      }
    }
  }
};
</script>

<style scoped>
.form-container {
  max-width: 400px;
  margin: 20px auto;
  padding: 15px;
  border: 1px solid #ccc;
  border-radius: 8px;
}

label {
  display: block;
  margin-top: 10px;
}

input {
  width: 100%;
  padding: 6px;
  margin-top: 4px;
}

button {
  margin-top: 15px;
  padding: 8px 12px;
  background: #42b983;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

button:hover {
  background: #369f6b;
}

.error {
  color: red;
  font-size: 0.9em;
}

.success {
  margin-top: 15px;
  padding: 10px;
  background: #e7f9ed;
  border: 1px solid #42b983;
  border-radius: 6px;
}
</style>
