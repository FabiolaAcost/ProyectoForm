<template>
  <div class="container mt-5">
    <form @submit.prevent="submitForm">
      <div class="form-group mb-3">
        <label for="name" class="text-center w-100">Nombre:</label>
        <input
          type="text"
          id="name"
          v-model="form.name"
          @input="validateName"
          class="form-control"
        />
        <p v-if="errors.name" class="text-danger">{{ errors.name }}</p>
      </div>

      <div class="form-group mb-3">
        <label for="email" class="text-center w-100">Correo:</label>
        <input
          type="email"
          id="email"
          v-model="form.email"
          @input="validateEmail"
          class="form-control"
        />
        <p v-if="errors.email" class="text-danger">{{ errors.email }}</p>
      </div>

      <div class="form-group mb-3">
        <label for="password" class="text-center w-100">Contraseña:</label>
        <input
          type="password"
          id="password"
          v-model="form.password"
          @input="validatePassword"
          class="form-control"
        />
        <p v-if="errors.password" class="text-danger">{{ errors.password }}</p>
      </div>

      <div class="form-group mb-3">
        <label for="confirmPassword" class="text-center w-100">Repetir Contraseña:</label>
        <input
          type="password"
          id="confirmPassword"
          v-model="form.confirmPassword"
          @input="validateConfirmPassword"
          class="form-control"
        />
        <p v-if="errors.confirmPassword" class="text-danger">{{ errors.confirmPassword }}</p>
      </div>

      <button type="submit" class="btn btn-success text-center">Enviar</button>
    </form>

    <p v-if="successMessage" class="text-success mt-3">{{ successMessage }}</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      form: {
        name: '',
        email: '',
        password: '',
        confirmPassword: '',
      },
      errors: {
        name: '',
        email: '',
        password: '',
        confirmPassword: '',
      },
      successMessage: '',
    };
  },
  methods: {
    validateName() {
      if (!this.form.name) {
        this.errors.name = 'El nombre es obligatorio.';
      } else if (/\d/.test(this.form.name)) {
        this.errors.name = 'El nombre no puede contener números.';
      } else {
        this.errors.name = '';
      }
    },
    validateEmail() {
      const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
      if (!this.form.email) {
        this.errors.email = 'El correo es obligatorio.';
      } else if (!emailRegex.test(this.form.email)) {
        this.errors.email = 'El correo no es válido.';
      } else {
        this.errors.email = '';
      }
    },
    validatePassword() {
      if (!this.form.password) {
        this.errors.password = 'El campo contraseña es requerido.';
      } else if (this.form.password.length < 5) {
        this.errors.password = 'La contraseña debe tener al menos 5 caracteres.';
      } else {
        this.errors.password = '';
      }
    },
    validateConfirmPassword() {
      if (!this.form.confirmPassword) {
        this.errors.confirmPassword = 'El campo repetir contraseña es requerido.';
      } else if (this.form.confirmPassword !== this.form.password) {
        this.errors.confirmPassword = 'Las contraseñas no coinciden.';
      } else {
        this.errors.confirmPassword = '';
      }
    },
    submitForm() {
      this.validateName();
      this.validateEmail();
      this.validatePassword();
      this.validateConfirmPassword();

      if (Object.values(this.errors).some((error) => error)) {
        return;
      }

      alert('El registro se ha realizado correctamente');
      
      this.form.name = '';
      this.form.email = '';
      this.form.password = '';
      this.form.confirmPassword = '';
    },
  },
};
</script>

<style scoped>
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