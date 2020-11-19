<template>
  <div class="container mt-4">
    <h2>Validaciones con Vuejs</h2>
    <form action="">
      <p>
        <label>Nombre :</label>
        <input
          type="text"
          class="form-control mb-4"
          name="nombre"
          placeholder="Escribir un nombre"
        />
      </p>
      <p>
        <label>Correo :</label>
        <input
          type="text"
          class="form-control"
          name="correo"
          placeholder="Escribir un correo"
        />
      </p>
      <p>
        <label>Teléfono :</label>
        <input
          type="text"
          class="form-control"
          name="telefono"
          placeholder="Escribir un teléfono"
        />
      </p>

       <p>
        <label>Mensaje :</label>
       <textarea name="mensaje" id="mensaje" cols="30" rows="10" class="form-control" placeholder="Escribe un mensaje ..."></textarea>
      </p>
      <hr>
      <input type="submit" value="Enviar datos" class="btn btn-success">
    </form>
  </div>
</template>

<script>
export default {
  name: "Form",
};
</script>

<style>
</style>