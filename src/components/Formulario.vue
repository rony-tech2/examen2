<template>
  <div>
    <h1>Formulario de prueba</h1>
    <div class="form">
      <form @submit.prevent="validarFormulario">
        <label>Nombre:</label>
        <input type="text" v-model="nombre" />

        <label>Edad:</label>
        <input type="number" v-model="edad" />

        <label>Dirección:</label>
        <input type="text" v-model="direccion" />

        <button type="submit">Enviar</button>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  name: "FormularioUser",

  data() {
    return {
      nombre: "",
      edad: "",
      direccion: "",
    };
  },

  methods: {
    validarFormulario() {
      try {
        const nombre = this.nombre.trim();
        const edad = Number(this.edad);
        const direccion = this.direccion.trim();

        // Validaciones
        if (!nombre || !edad || !direccion) {
          return alert("Por favor, completa todos los campos.");
        }

        if (isNaN(edad) || edad < 15 || edad > 80) {
          return alert("La edad debe ser un número válido entre 15 y 80.");
        }

        if (!/^[a-zA-Z\s]+$/.test(nombre)) {
          return alert("El nombre solo puede contener letras y espacios.");
        }

        if (direccion.length < 5) {
          return alert("La dirección debe tener al menos 5 caracteres.");
        }

        // Si todo es válido
        alert(
          ` Datos recibidos:\nNombre: ${nombre}\nEdad: ${edad}\nDirección: ${direccion}`
        );

        // 🧹 Limpiar los campos del formulario
        this.limpiarFormulario();
      } catch (error) {
        console.error("Error al validar el formulario:", error);
        alert("Ocurrió un error al validar el formulario.");
      }
    },

    // Nuevo método para limpiar campos
    limpiarFormulario() {
      this.nombre = "";
      this.edad = "";
      this.direccion = "";
    },
  },
};
</script>

<style scoped>
.form {
  max-width: 420px;
  margin: 60px auto;
  padding: 25px;
  background: rgba(255, 255, 255, 0.2);
  border: 1px solid rgba(255, 255, 255, 0.3);
  border-radius: 16px;
  backdrop-filter: blur(10px);
  box-shadow: 0 8px 20px rgba(0, 0, 0, 0.15);
  font-family: "Poppins", sans-serif;
  color: #222;
}

.form label {
  display: block;
  margin-bottom: 8px;
  font-weight: 600;
  color: #333;
  letter-spacing: 0.5px;
}

.form input {
  width: 100%;
  padding: 12px;
  margin-bottom: 18px;
  border: 1px solid rgba(0, 0, 0, 0.2);
  border-radius: 8px;
  background: rgba(255, 255, 255, 0.6);
  font-size: 15px;
  box-sizing: border-box;
  outline: none;
  transition: all 0.3s ease;
}

.form input:focus {
  border-color: #4a90e2;
  box-shadow: 0 0 6px rgba(74, 144, 226, 0.4);
  background-color: #fff;
}

.form button {
  width: 100%;
  padding: 12px;
  background: linear-gradient(135deg, #4a90e2, #00c6ff);
  color: white;
  border: none;
  border-radius: 8px;
  font-size: 17px;
  font-weight: 600;
  cursor: pointer;
  transition: transform 0.2s ease, background 0.3s ease;
}

.form button:hover {
  transform: translateY(-2px);
  background: linear-gradient(135deg, #00c6ff, #4a90e2);
}
</style>
