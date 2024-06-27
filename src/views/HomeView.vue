<template>
  <div class="main-container">
    <h1>Cadastrar veículos</h1>
    <CarForm />
  </div>
</template>

<script>
import CarForm from "../components/CarForm.vue";
export default {
  components: {
    CarForm,
  },
};
</script>
