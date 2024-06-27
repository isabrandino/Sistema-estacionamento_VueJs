<template>
  <div id="nav">
    <router-link to="/" id="logo-url">
      <img :src="logo" :alt="alt" id="logo" />
    </router-link>

    <router-link to="/">Home</router-link>
    <router-link to="/cadastro">Cadastro</router-link>
  </div>
</template>

<script>
export default {
  name: "Navbar",
  props: ["logo", "alt"], // logo e imagem do projeto
};
</script>

<style scoped>
#nav {
  background-color: #3f7fbf;
  padding: 15px 50px;
  display: flex;
  justify-content: flex-end;
  align-items: center;
}

#nav #logo-url {
  margin: auto;
  margin-left: 0;
}

#logo {
  width: 40px;
  height: 40px;
}

#nav a {
  color: #fff;
  text-decoration: none;
  margin: 12px;
  transition: 0.5s;
  font-size: 20px;
  font-family: Arial, Arial, Helvetica, sans-serif;
}

#nav a:hover {
  color: #222;
}
</style>
