<template>
  <div>
    <nav class="navbar navbar-expand bg-light w-100">
      <div class="container-fluid">
        <a class="navbar-brand" href="#">Programación Front End</a>
        <ul class="navbar-nav me-auto mb-2 mb-lg-0">
          <li class="nav-item">
            <router-link class="nav-link" to="/" exact>
              Cálculo de calificaciones
            </router-link>
          </li>
          <li class="nav-item">
            <router-link class="nav-link" to="/registro">
              Formulario de registro
            </router-link>
          </li>
          <li class="nav-item">
            <a class="nav-link disabled" aria-disabled="true">En construcción</a>
          </li>
        </ul>
        <form class="d-flex ms-auto" role="search">
          <input
            class="form-control me-2"
            type="search"
            placeholder="Search"
            aria-label="Search"
          />
          <button class="btn btn-outline-success" type="submit">Búsqueda</button>
        </form>
      </div>
    </nav>
    <div class="container mt-5">
      <router-view></router-view>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
};
</script>

<style scoped>
.navbar {
  width: 100%;
  position: relative;
}

.navbar {
  background-color: #004203; 
  border-bottom: 2px solid #38424d; 
}

.navbar a {
  font-weight: bold; 
}

.navbar a:hover {
  color: #00670e; 
  text-decoration: underline; 
}

.navbar .btn-outline-success {
  border-color: #fff;
}

.navbar .btn-outline-success:hover {
  background-color: #6cb179;
  color: #e8e8e8;
}
</style>
