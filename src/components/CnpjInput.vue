<template>
  <div v-if="!data" class="container flex center column">
    <h1>Consultar CNPJ</h1>
    <div class="input flex center">
      <input
        type="text"
        placeholder="Digite o CNPJ"
        v-model="cnpj"
        v-mask="['##.###.###/####-##']"
        @change="handleChange"
      />
      <button @click="handleInput">Consultar</button>
    </div>
    <span class="error" v-if="error">{{error}}</span>
  </div>
  <CnpjDetails v-if="data" :data="data" @newQuery="handleNewQuery" />
</template>

<script>
import axios from "axios";
import CnpjDetails from "./CnpjDetails.vue";
import { mask } from "vue-the-mask";
export default {
  data() {
    return {
      cnpj: null,
      data: null,
      error:null
    };
  },
  directives: { mask },
  components: { CnpjDetails },
  methods: {
    handleNewQuery(){
      this.data = null
      this.cnpj = null
    },
    handleInput() {
      const Regex = /^\d{2}\.\d{3}\.\d{3}\/\d{4}-\d{2}$/
      if(!Regex.test(this.cnpj)) {
        this.error = 'CNPJ inválido'
      }else {        
        axios
          .get(
            `https://api-publica.speedio.com.br/buscarcnpj?cnpj=${this.cnpj
              .replace(/\./g, "")
              .replace(/-/g, "")
              .replace(/\//g, "")}`
          )
          .then((response) => {
            if(response.data.error) {
               this.error = 'CNPJ inválido'
            }else {
              this.data = response.data;
              this.params = Object.keys(response.data);
            }
            
          })
          .catch(console.log);
      }
    },
    handleChange() {
      this.error = null
    }
  },
  name: "CnpjInput",
  props: {
    msg: String,
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.container {
  width: 100vw;
  height: 100vh;
}
.container h1 {
  padding: 50px;
  font-size: 4rem;
}
.input input {
  font-size: 1.4rem;
  outline:none;
  padding: 10px 16px;
}
.input button {
  font-size: 1.4rem;
  outline:none;
  padding: 10px 16px;
}
.error {
  margin-top: 5px;
  color: black;
}
.flex {
  display: flex;
}
.center {
  align-items:center;
  justify-content: center;
}
.around {
  align-items:center;
  justify-content: space-around;
}
.column {
  flex-direction: column;
}
.row {
  flex-direction: row;
}
.data {
  padding: 40px;
  width: 100%
}
ul {
 margin-top: 16px;
}
</style>
