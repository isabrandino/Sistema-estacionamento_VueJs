<template>
  <div class="mensagem-container">
    <h2> {{ msg }} </h2>
  </div>
</template>

<script>
export default {
  name: "Mensagem",

  props: {
    msg: String
  }
  
}
</script>

<style scoped>
.mensagem-container {
  color: white;
  background-color: #7f7e7e;
  border: 2px solid #9d9fa0;
  border-radius: 5px;
  padding: 6px;
  max-width: 350px;
  margin: 30px auto;
}
</style>