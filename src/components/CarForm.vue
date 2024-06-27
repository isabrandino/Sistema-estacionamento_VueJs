<template>
  <div>
    <Mensagem :msg="msg" v-show="msg"/>

    <form id="car-form" @submit="createCar">
      <div class="input-container">
        <label for="nome">Nome para Cadastro:</label>
        <input
          type="text"
          id="nome"
          v-model="nome"
          placeholder="Informe o seu nome"
        />
      </div>

      <div class="input-container">
        <label for="nomeCar">Modelo do Veículo:</label>
        <input
          type="text"
          id="nomeCar"
          v-model="nomeCar"
          placeholder="Informe o modelo do veículo"
        />
      </div>

      <div class="input-container">
        <label for="placaCar">Placa de Identificação:</label>
        <input
          type="text"
          id="placaCar"
          v-model="placaCar"
          placeholder="Informe a placa do carro"
        />
      </div>

      <div class="input-container">
        <label for="hora">Horário de Entrada:</label>
        <input
          type="text"
          id="hora"
          v-model="hora"
          placeholder="Informe o horário de entrada"
        />
      </div>

      <div class="input-container">
        <input type="submit" class="submit-btn" value="Cadrastrar o Veículo" />
      </div>
    </form>
  </div>
</template>

<script>

import Mensagem from './Mensagem.vue';

export default {
  name: "CarForm",
  data() {
    return {
      nome: null,
      nomeCar: null,
      placaCar: null,
      hora: null,
      msg: null,
    };
  },
  methods: {
    async createCar(e) {
      e.preventDefault();
      
      const data = {
        nome: this.nome,
        nomeCar: this.nomeCar,
        placaCar: this.placaCar,
        hora: this.hora,
        status: "Solicitado",
      }

      //console.log(data)

      const dataJson = JSON.stringify(data);

      //fazendo um post

        const req = await fetch ("http://localhost:3000/carros", {
          method: "POST",
          header: {"Content-type" : "application/json"},
          body:dataJson
        });

        const res = await req.json();
        console.log(res);

        //Mensagem de cadastro
        this.msg = `  Veículo cadastrado com sucesso!`;

        //limpar a mensagem
        setTimeout(() => this.msg = "",3000)

        //Limpar campos
        this.nome = "";
        this.nomeCar = "";
        this.placaCar = "";
        this.hora = "";
    },
  },

  components: {
    Mensagem
  }

};
</script>

<style scoped>
#car-form {
  max-width: 1000px;
  margin: 0 auto;
  width: 500px;
}

.input-container {
  display: flex;
  flex-direction: column;
  margin-bottom: 20px;
}

label {
  font-weight: bold;
  margin-bottom: 10px;
  color: #222;
  padding: 5px 10px;
  border-left: 4px solid #3f7fbf;
}

input {
  padding: 5px 10px;
  border-radius: 4px;
}

.submit-btn {
  background-color: #3f7fbf;
  color: white;
  font-weight: bold;
  padding: 10px;
  font-size: 16px;
  border: 2px solid white;
  cursor: pointer;
  transition: 0.5s;
  border-radius: 8px;
}

.submit-btn:hover {
  background-color: #222;
  font-size: 18px;
}
</style>
