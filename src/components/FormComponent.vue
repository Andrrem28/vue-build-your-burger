<template>
  <div>
    <MessageComponent :msg="msg" v-show="msg" />
    <div>
      <form id="burguer-form" @submit="createBurguer">
        <div class="input-container">
          <label for="customer_name">Nome do Cliente</label>
          <input
            type="text"
            id="customer_name"
            name="name"
            v-model="name"
            placeholder="Digite o seu nome"
          />
        </div>
        <div class="input-container">
          <label for="type_bread">Escolha o tipo de pão:</label>
          <select name="bread" id="type_bread" v-model="bread">
            <option value="">Selecione...</option>
            <option v-for="bread in breads" :key="bread.id" :value="bread.type">
              {{ bread.type }}
            </option>
          </select>
        </div>
        <div class="input-container">
          <label for="type_meat">Escolha o tipo de carne:</label>
          <select name="meat" id="type_meat" v-model="meat">
            <option value="">Selecione...</option>
            <option
              v-for="meat in type_of_meat"
              :key="meat.id"
              :value="meat.type"
            >
              {{ meat.type }}
            </option>
          </select>
        </div>
        <div id="additional-container" class="input-container">
          <label>Incremente seu sanduíche:</label>
          <div
            class="checkbox-container"
            v-for="additional in more_options"
            :key="additional.id"
          >
            <input
              id="additional-title"
              type="checkbox"
              name="additional"
              :value="additional.type"
              :v-model="more_options"
            />
            <span>{{ additional.type }}</span>
          </div>
        </div>
        <div class="input-container">
          <input class="submit-btn" type="submit" value="Criar meu sanduíche" />
        </div>
      </form>
    </div>
  </div>
</template>

<script>
import MessageComponent from "./MessageComponent.vue";
export default {
  name: "Burguer-form",
  data() {
    return {
      breads: null,
      type_of_meat: null,
      more_options: [],
      name: null,
      bread: null,
      meat: null,
      additional: null,
      msg: null,
    };
  },
  components: {
    MessageComponent,
  },
  methods: {
    async getIngredients() {
      const request = await fetch("http://localhost:3000/ingredients");
      const data = await request.json();

      this.breads = data.breads;
      this.type_of_meat = data.type_of_meat;
      this.more_options = data.more_options;
    },
    async createBurguer(event) {
      event.preventDefault();
      const data = {
        name: this.name,
        bread: this.bread,
        meat: this.meat,
        more_options: Array.from(this.more_options),
        status: "Solicitado",
      };
      const dataJson = JSON.stringify(data);
      const request = await fetch("http://localhost:3000/burgers", {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: dataJson,
      });

      const res = await request.json();
      /** Criar tratamento de erro, para requisição POST */

      this.name = "";
      this.meat = "";
      this.bread = "";
      this.additional = "";
      this.msg = `Pedido de Nº ${res.id} realizado com sucesso!`;

      setTimeout(() => (this.msg = ""), 5000);
    },
  },
  mounted() {
    this.getIngredients();
  },
};
</script>

<style scoped>
#burguer-form {
  max-width: 400px;
  margin: 0 auto;
}
.input-container {
  display: flex;
  flex-direction: column;
  margin-bottom: 10px;
}
label {
  font-weight: bold;
  margin-bottom: 15px;
  color: #222;
  padding: 5px 10px;
  border-left: 4px solid #fcba03;
}
input,
select {
  padding: 5px 10px;
  width: 400px;
}
#additional-container {
  flex-direction: row;
  flex-wrap: wrap;
}
.checkbox-container {
  display: flex;
  align-items: flex-start;
  width: 50%;
  margin-bottom: 20px;
}
.checkbox-container span,
.checkbox-container input {
  width: 20%;
}
.checkbox-container span {
  font-weight: bold;
}
.submit-btn {
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
.submit-btn:hover {
  background-color: #fff;
}
</style>
