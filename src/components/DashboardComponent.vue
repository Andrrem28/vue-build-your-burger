<template>
  <div id="burger-table" v-if="burgers && burgers.length > 0">
    <MessageComponent :msg="msg" v-show="msg" />
    <div>
      <div id="burger-table-heading">
        <div class="order-id">#:</div>
        <div>Cliente:</div>
        <div>Pão:</div>
        <div>Carne:</div>
        <div>Opcionais:</div>
        <div>Ações:</div>
      </div>
    </div>
    <div id="burger-table-rows">
      <div class="burger-table-row" v-for="burger in burgers" :key="burger.id">
        <div class="order-number">{{ burger.id }}</div>
        <div>{{ burger.name }}</div>
        <div>{{ burger.bread }}</div>
        <div>{{ burger.meat }}</div>
        <div>
          <ul>
            <li v-for="(additional, index) in burger.more_options" :key="index">
              {{ additional }}
            </li>
          </ul>
        </div>
        <div>
          <select
            name="status"
            class="status"
            @change="updateOrder($event, burger.id)"
          >
            <option>Selecione...</option>
            <option
              v-for="situation in status"
              :value="situation.type"
              :key="situation.id"
              :selected="burger.status == situation.type"
            >
              {{ situation.type }}
            </option>
          </select>
          <button class="delete-btn" @click="deleteOrder(burger.id)">
            Cancelar
          </button>
        </div>
      </div>
    </div>
  </div>
  <div v-else>
    <h2>Não há pedidos no momento!</h2>
  </div>
</template>
<script>
import MessageComponent from "./MessageComponent.vue";

export default {
  name: "Dashboard-component",
  data() {
    return {
      burgers: null,
      burger_id: null,
      status: [],
    };
  },

  components: {
    MessageComponent,
  },

  methods: {
    async getOrders() {
      const request = await fetch("http://localhost:3000/burgers");
      const data = await request.json();

      this.burgers = data;
    },

    async getStatus() {
      const request = await fetch("http://localhost:3000/status");
      const data = await request.json();

      this.status = data;
    },

    async updateOrder(event, id) {
      const option = event.target.value;

      const dataJson = JSON.stringify({ status: option });

      const request = await fetch(`http://localhost:3000/burgers/${id}`, {
        method: "PATCH",
        headers: { "Content-Type": "application/json" },
        body: dataJson,
      });
      const response = await request.json();
      this.msg = `Pedido de código ${response.id} atualizado para (${response.status}) sucesso!`;

      /** Limpa a mensagem depois de 5 segundos */
      setTimeout(() => (this.msg = ""), 5000);
    },

    async deleteOrder(id) {
      const request = await fetch(`http://localhost:3000/burgers/${id}`, {
        method: "DELETE",
      });

      const response = await request.json();
      this.msg = `Pedido de código ${response.id} removido com sucesso!`;

      /** Limpa a mensagem depois de 5 segundos */
      setTimeout(() => (this.msg = ""), 5000);
      this.getOrders();
    },
  },

  mounted() {
    this.getOrders();
    this.getStatus();
  },
};
</script>

<style scoped>
#burger-table {
  max-width: 1200px;
  margin: 0 auto;
}

#burger-table-heading,
#burger-table-rows,
.burger-table-row {
  display: flex;
  flex-wrap: wrap;
}

#burger-table-heading {
  font-weight: bold;
  padding: 12px;
  border-bottom: 3px solid #333;
}

.burger-table-row {
  width: 100%;
  padding: 12px;
  border-bottom: 1px solid #ccc;
}

#burger-table-heading div,
.burger-table-row div {
  width: 19%;
}

#burger-table-heading .order-id,
.burger-table-row .order-number {
  width: 5%;
}

select {
  padding: 12px 6px;
  margin-right: 12px;
}

.delete-btn {
  background-color: #222;
  color: #fcba03;
  font-weight: bold;
  border: 2px solid #222;
  padding: 10px;
  font-size: 16px;
  margin: 0 auto;
  cursor: pointer;
  transition: 0.5s;
}

.delete-btn:hover {
  background-color: transparent;
  color: #222;
}
</style>
