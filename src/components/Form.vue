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
            <label>Seleccionar tu país</label>
           <!-- <select class="form-control form-control-lg" > -->
               <select class="form-control" v-model.trim="contacto.pais" >
                <option value="" >Selecciona tu país</option>
                <option  v-for="c in listaPaises" :value="c.alpha3Code" :key="c.alpha3Code"  >
                     {{ c.name }} 
                </option>
            </select>
        </p>
             <div v-if="submited && !$v.contacto.pais.required" class="alert alert-danger">La selección es requerida</div>

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
    <p>
        <label>Edad :</label>
        <input
          type="number"
          class="form-control"
          name="edad"
          v-model="contacto.edad"
          placeholder="Escribir su edad"
        />
      </p>
                 <div v-if="submited && !$v.contacto.edad.required" class="alert alert-danger">El campo edad es requerido</div>

          <div v-if="submited && !$v.contacto.edad.between" class="alert alert-danger">El campo edad no puede ser menor a 18 ni mayor a 80</div>
         <p>
        <label>Url :</label>
        <input
          type="text"
          class="form-control"
          name="url"
          v-model="contacto.url"
          placeholder="Ingresar tu url de página"
        />
      </p>
                <div v-if="submited && !$v.contacto.url.url" class="alert alert-danger">Ingrese una url válida</div>


<p>
        <label>Escribe cool :</label>
        <input
          type="text"
          class="form-control"
          name="cools"
          v-model="contacto.cools"
          placeholder="Escribe cool"
          maxlength="4"
        />
      </p>
                <div v-if="submited && !$v.contacto.cools.mustBeCool" class="alert alert-danger">No ha escrito cool</div>

      <hr />
      <input type="submit" value="Enviar datos" class="btn btn-success" />
    </form>
  </div>
</template>

<script>
//2
import { required, minLength, email, maxLength ,between,url } from 'vuelidate/lib/validators';
//ejecuta binding
const mustBeCool = (value) => value.indexOf('cool') >= 0
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
        mensaje: '',
        pais : '',
        edad : '',
        url : '',
        cools: ''
       
      },
       listaPaises: []
    };
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
      },
        pais: {
        required
       
      },
       edad: {
        required,
        between: between(18,80)
       
      },
      url: {
        url
       
      },
      cools: {
          mustBeCool
      }
    }
  },

  //llamado a los paises
  mounted: function(){
      var v = this;
      v.$http.get('https://restcountries.eu/rest/v2/all')
      .then(function(resp){
          v.listaPaises = resp.data;
      })
      .catch(function(err){
          console.log(err)
      });
  },
  methods: {
      formateardata: function(){
          this.nombre= '';
          this.telefono='';
          this.pais='';
          this.mensaje='';
      },
    procesar() {
        this.submited = true;
        this.$v.$touch();
      if (this.$v.$invalid) {
        return false;
      }
      alert('Data enviada');
      
    //  this.formateardata();
    }
  }
}
</script>

<style>
</style>