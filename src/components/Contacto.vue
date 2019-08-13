<template>
  <div class="contacto">
      <h2>{{nombre}}</h2>
      <h3>{{correo}}</h3>
  </div>
</template>

<script>
export default {
  name: 'Contacto',
  props : {
      nombre : String,
      correo : String
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>