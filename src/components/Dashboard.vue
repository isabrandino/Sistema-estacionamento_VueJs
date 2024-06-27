<template>
  <div id="car-table">
    <Mensagem :msg="msg" v-show="msg" />

    <div id="car-table-heading">
      <div class="column order-id">#:</div>
      <div class="column">Nome para Cadastro:</div>
      <div class="column">Modelo do Veículo:</div>
      <div class="column">Placa de Identificação:</div>
      <div class="column">Horário de Entrada:</div>
      <div class="column actions">Ações:</div>
    </div>

    <div id="car-table-rows">
      <div class="car-table-row" v-for="carro in carros" :key="carro.id">
        <div class="column order-number">{{ carro.id }}</div>
        <div class="column">{{ carro.nome }}</div>
        <div class="column">{{ carro.nomeCar }}</div>
        <div class="column">{{ carro.placaCar }}</div>
        <div class="column">{{ carro.hora }}</div>

        <div class="column actions">
          <select
            name="status"
            class="status"
            @change="updateCarro($event, carro.id)"
          >
            <option value="">Status do Veículo</option>
            <option
              :value="statu.tipo"
              v-for="statu in status"
              :key="statu.id"
              :selected="carro.status == statu.tipo"
            >
              {{ statu.tipo }}
            </option>
          </select>
          <button class="delete-btn" @click="deletarCarro(carro.id)">
            Eliminar reserva
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>

  import Mensagem from './Mensagem.vue';

export default {
  name: "Dashboard",

  data() {
    return {
      carros: null,
      carros_id: null,
      status: [],
      msg: null
    };
  },

    components : {
      Mensagem
    },

  methods: {
    async getCadastros() {
      const req = await fetch("http://localhost:3000/carros");

      const data = await req.json();

      this.carros = data;

      this.getStatus();
    },

    async getStatus() {
      const req = await fetch("http://localhost:3000/status");

      const data = await req.json();

      this.status = data;
    },

    async deletarCarro(id) {
      const req = await fetch(`http://localhost:3000/carros/${id}`, {
        method: "DELETE",
      });

      const data = await req.json();

      //Mensagem de cadastro
        this.msg = `Reserva eliminada com sucesso!`;

        //limpar a mensagem
        setTimeout(() => this.msg = "",3000)

      this.getCadastros();
    },

    //Atualizando o status
    async updateCarro(event, id) {
      const opcoes = event.target.value;
      const dataJson = JSON.stringify({ status: opcoes });
      const req = await fetch(`http://localhost:3000/carros/${id}`, {
        method: "PATCH",
        headers: { "content-Type": "application/json" },
        body: dataJson,
      });

      const res = await req.json();

      //Mensagem de cadastro
        this.msg = `  O status do veículo de ${res.nome} foi atualizado para ${res.status}.`;

        //limpar a mensagem
        setTimeout(() => this.msg = "",3000)

      console.log(res);
    },
  },

  mounted() {
    this.getCadastros();
  },
};
</script>

<style scoped>
#car-table {
  max-width: 1200px;
  margin: 0 auto;
}

#car-table-heading,
#car-table-rows .car-table-row {
  display: flex;
}

#car-table-heading {
  font-weight: bold;
  padding: 12px;
  border-bottom: 3px solid #3f7fbf;
}

.column {
  flex: 1;
  padding: 8px;
}

.order-id,
.order-number {
  flex: 0 0 5%;
  min-width: 50px;
}

.actions {
  display: flex;
  align-items: center;
  justify-content: flex-start;
}

.actions select {
  margin-right: 10px;
}

.delete-btn {
  background-color: #3f7fbf;
  color: white;
  font-weight: 500;
  padding: 8px;
  font-size: 14px;
  border: 2px solid white;
  cursor: pointer;
  transition: 0.5s;
  border-radius: 8px;
}

.delete-btn:hover {
  background-color: #222;
  font-size: 17px;
}

.car-table-row {
  padding: 12px;
  border-bottom: 1px solid #3f7fbf;
}

select {
  padding: 6px 1px;
}
</style>
