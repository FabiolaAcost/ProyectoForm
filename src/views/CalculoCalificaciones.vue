<template>
  <div class="container mt-5">
    <form @submit.prevent="calcularPromedio">
      <div class="form-group mb-3">
        <label for="nota1" class="text-center w-100">Nota 1</label>
        <input
          type="number"
          id="nota1"
          v-model="notas.nota1"
          @input="validarCampo('nota1')"
          class="form-control"
          placeholder="nota 1"
        />
        <p v-if="errores.nota1">{{ errores.nota1 }}</p>
      </div>

      <div class="form-group mb-3">
        <label for="nota2" class="text-center w-100">Nota 2</label>
        <input
          type="number"
          id="nota2"
          v-model="notas.nota2"
          @input="validarCampo('nota2')"
          class="form-control"
          placeholder="nota 2"
        />
        <p v-if="errores.nota2" >{{ errores.nota2 }}</p>
      </div>

      <div class="form-group mb-3">
        <label for="nota3" class="text-center w-100">Nota 3</label>
        <input
          type="number"
          id="nota3"
          v-model="notas.nota3"
          @input="validarCampo('nota3')"
          class="form-control"
          placeholder="nota 3"
        />
        <p v-if="errores.nota3" >{{ errores.nota3 }}</p>
      </div>

      <div class="form-group mb-3">
        <label for="asistencia" class="text-center w-100">Asistencia %</label>
        <input
          type="number"
          id="asistencia"
          v-model="asistencia"
          @input="validarCampo('asistencia')"
          class="form-control"
          placeholder="asistencia"
        />
        <p v-if="errores.asistencia" >{{ errores.asistencia }}</p>
      </div>

      <div class="text-center">
        <button type="submit" class="btn btn-primary">Calcular</button>
      </div>
    </form>

    <p v-if="mensajeGlobal" class="text-danger mt-3 text-center">{{ mensajeGlobal }}</p>

    <p v-if="resultado.mensaje" :class="resultado.clase" class="mt-3 text-center" v-html="resultado.mensaje"></p>

  </div>
</template>

<script>
export default {
  data() {
    return {
      notas: { nota1: '', nota2: '', nota3: '' },
      asistencia: '',
      errores: { nota1: '', nota2: '', nota3: '', asistencia: '' },
      resultado: { mensaje: '', clase: '' },
      mensajeGlobal: '', 
    };
  },
  methods: {
    validarCampo(campo) {
      const valor = this.notas[campo] || this.asistencia;
      let error = '';

      if (campo === 'asistencia') {
        if (!valor || valor < 0) {
          error = 'El valor debe ser superior o igual a 0.';
        } else if (valor > 100) {
          error = 'El valor debe ser inferior o igual a 100.';
        }
      } else {
        if (!valor || valor < 10) {
          error = 'El valor debe ser superior o igual a 10.';
        } else if (valor > 70) {
          error = 'El valor debe ser inferior o igual a 70.';
        }
      }

      this.errores[campo] = error;

      this.actualizarMensajeGlobal();
    },
    actualizarMensajeGlobal() {
      const hayErrores = Object.values(this.errores).some((error) => error !== '');
      this.mensajeGlobal = hayErrores
        ? 'Por favor, ingrese valores válidos para las notas y la asistencia.'
        : '';
    },
    calcularPromedio() {
      this.validarCampo('nota1');
      this.validarCampo('nota2');
      this.validarCampo('nota3');
      this.validarCampo('asistencia');

      const hayErrores = Object.values(this.errores).some((error) => error !== '');
      if (hayErrores) {
        this.mensajeGlobal = 'Por favor, ingrese valores válidos para las notas y la asistencia.';
        return;
      }

      this.mensajeGlobal = ''; 

      const promedio =
        this.notas.nota1 * 0.35 +
        this.notas.nota2 * 0.35 +
        this.notas.nota3 * 0.3;

      if (promedio >= 40 && this.asistencia >= 80) {
        this.resultado = {
          mensaje: `El promedio es: ${promedio.toFixed(2)} <br>
           Tu estado es: Aprobado`,
          clase: 'text-center',
        };
      } else {
        this.resultado = {mensaje: `El promedio es: ${promedio.toFixed(2)}<br>
           Tu estado es: Reprobado`,
          clase: 'text-center',
        };
      }
    },
  },
};
</script>

<style scoped>
.text-danger {
  color: #dc3545;
}

form {
  background-color: #f8f9fa; 
  padding: 20px; 
  border-radius: 10px; 
  box-shadow: 0px 4px 10px rgba(0, 0, 0, 0.1); 
}

form label {
  font-weight: bold; 
  color: #333; 
}

form input {
  border-radius: 5px; 
  padding: 10px; 
  font-size: 14px; 
}

form input:focus {
  outline: none; 
  border-color: #004014; 
  box-shadow: 0px 0px 5px #4e7d4f; 
}

form button {
  background-color: #075f16; 
  color: #fff; 
  border: none;
  padding: 10px 20px;
  border-radius: 5px;
}

form button:hover {
  background-color: #53af65; 
}
</style>
