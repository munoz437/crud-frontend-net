<template>
  <div class="container">
    <div class="card">
      <div class="card-header">
        Agrega nuevo empleado
      </div>
      <div class="card-body">
        <form v-on:submit.prevent="agregarEmpleado">
          <div class="mb-3">
            <label for="codigo" class="form-label">Código:</label>
            <input
              type="text"
              class="form-control"
              name="codigo"
              v-model="empleado.codigo"
              id="codigo"
              placeholder="E001"
            />
          </div>
          <div class="mb-3">
            <label for="nombres" class="form-label">Nombres:</label>
            <input
              type="text"
              class="form-control"
              name="nombres"
              v-model="empleado.nombres"
              id="nombres"
              placeholder="Nombres"
            />
          </div>
          <div class="mb-3">
            <label for="apellidos" class="form-label">Apellidos:</label>
            <input
              type="text"
              class="form-control"
              name="apellidos"
              v-model="empleado.apellidos"
              id="apellidos"
              placeholder="Apellidos"
            />
          </div>
          <div class="mb-3">
            <label for="direccion" class="form-label">Dirección:</label>
            <input
              type="text"
              class="form-control"
              name="direccion"
              v-model="empleado.direccion"
              id="direccion"
              placeholder="Calle #1"
            />
          </div>
          <div class="mb-3">
            <label for="telefono" class="form-label">Teléfono:</label>
            <input
              type="text"
              class="form-control"
              name="telefono"
              v-model="empleado.telefono"
              valueid="telefono"
              placeholder="1290-6078"
            />
          </div>
          <div class="mb-3">
            <label for="fecha_nacimiento" class="form-label"
              >Fecha de nacimiento:</label
            >
            <input
              type="date"
              class="form-control"
              name="fecha_nacimiento"
              v-model="empleado.fecha_nacimiento"
              valueid="fecha_nacimiento"
              placeholder="2000/03/11"
            />
          </div>
          <div class="mb-3">
            <label for="puesto" class="form-label">Puesto:</label>
            <select v-model="empleado.id_puesto" class="form-select">
              <option v-for="puesto in puestos" v-bind:key="puesto.id_puesto" v-bind:value="puesto.id_puesto">
                {{ puesto.puesto }}
              </option>
            </select>
          </div>
          <div class="btn-group" role="group" aria-label="">
            <button type="submit" class="btn btn-success">
              Agregar
            </button>
            <router-link to="/empleados/ListarEmpleados" class="btn btn-danger"
              >Cancelar</router-link
            >
          </div>
        </form>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      empleado: {},
      puestos: []
    };
  },
  created: function() {
    this.consultarPuestos();
  },
  methods: {
    consultarPuestos() {
      fetch("https://localhost:5001/api/puestos")
        .then((response) => response.json())
        .then((dataResponsive) => {
          this.puestos = [];
          this.puestos = dataResponsive;
        })
        .catch(console.log);
    },
    agregarEmpleado() {
      const e = {
        //id_empleado: this.empleado.id_empleado,
        codigo: this.empleado.codigo,
        nombres: this.empleado.nombres,
        apellidos: this.empleado.apellidos,
        direccion: this.empleado.direccion,
        telefono: this.empleado.telefono,
        fecha_nacimiento: this.empleado.fecha_nacimiento,
        id_puesto: this.empleado.id_puesto,
      };
      
      fetch("https://localhost:5001/api/empleados", {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify(e),
      })
        //.then((response) => response.json())
        .then((dataResponsive) => {
          console.log(dataResponsive);
          window.location.href = "ListarEmpleados";
        });
    },
  },
};
</script>
