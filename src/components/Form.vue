<template>
  <div class="container mt-4">
    <h2>Validaciones con Vuejs</h2>
    <!--directiva v-on || gestor de eventos || activamos ese evento que cuando se haga submit recoja el evento-->
    <form name="form" id="form" v-on:submit.prevent="procesar();">
      <p>
        <label>Nombre :</label>
        <input
          type="text"
          class="form-control mb-4"
          name="nombre"
          v-model="contacto.nombre"
          placeholder="Escribir un nombre"
          autocomplete="off"
        />
      </p>
        <div v-if="submited && !$v.contacto.nombre.required" class="alert alert-danger">El campo nombre es obligatorio</div>
          <div v-if="submited && !$v.contacto.nombre.minLength" class="alert alert-danger">El campo nombre debe tener al menos 2 caracteres</div>
      <p>
        <label>Correo :</label>
        <input
          type="text"
          class="form-control"
          name="correo"
          v-model="contacto.correo"
          placeholder="Escribir un correo"
        />
      </p>
      <div v-if="submited && !$v.contacto.correo.required" class="alert alert-danger">El campo nombre es obligatorio</div>
          <div v-if="submited && !$v.contacto.correo.email" class="alert alert-danger">Ingrese un email válido</div>
      <p>
        <label>Teléfono :</label>
        <input
          type="number"
          class="form-control"
          name="telefono"
          v-model="contacto.telefono"
          placeholder="Escribir un teléfono"
        />
      </p>
     <div v-if="submited && !$v.contacto.telefono.required" class="alert alert-danger">El campo teléfono es requerido</div>
     <div v-if="submited && !$v.contacto.telefono.maxLength" class="alert alert-danger">El campo telefono no debe superar los 9 dígitos</div>

      <p>
        <label>Mensaje :</label>
        <textarea
          name="mensaje"
          id="mensaje"
          cols="30"
          rows="10"
          v-model="contacto.mensaje"
          class="form-control"
          placeholder="Escribe un mensaje ..."
        ></textarea>
      </p>
           <div v-if="submited && !$v.contacto.mensaje.required" class="alert alert-danger">El campo mensaje es requerido</div>

    <div v-if="submited && !$v.contacto.mensaje.maxLength" class="alert alert-danger">El campo mensaje no debe superar los 300 caracteres</div>

      <hr />
      <input type="submit" value="Enviar datos" class="btn btn-success" />
    </form>
  </div>
</template>

<script>
//2
import { required, minLength, email, maxLength} from 'vuelidate/lib/validators';
//ejecuta binding
export default {
  name: "Form",
  data() {
    return {
      //1. creo mi objeto y lo asocio a mis inputs , eso es hacer binding
      submited: false,
      contacto: {
        nombre: '',
        correo: '',
        telefono: '',
        mensaje: ''
      },
    };
  },
  methods: {
    procesar() {
        this.submited = true;
        this.$v.$touch();
      if (this.$v.$invalid) {
        return false;
      }
      alert(this.contacto.nombre);
    }
  },
  //3
  validations: {
    contacto: {
      nombre: {
        required,
        minLength: minLength(2)
      },
      correo: {
        required,
        minLength: minLength(2),
        email
      },
      telefono: {
        required,
        maxLength: maxLength (9)
      },
        mensaje: {
        required,
        maxLength: maxLength (300)
      }
    }
  }
}
</script>

<style>
</style>