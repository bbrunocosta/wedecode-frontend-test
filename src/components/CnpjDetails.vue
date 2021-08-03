<template>
  <div class="container flex center column">
    <h1> Resultado da busca</h1>
    <div class="data" v-if="data">
      <ul class="flex around">
        <Field
          title="CNPJ"
          :data="data['CNPJ']"
          :mask="['##.###.###/####-##']"
          width="220px"
        />
        <Field title="Status" :data="data['STATUS']" width="130px" />
        <Field title="Aberto em" :data="data['DATA ABERTURA']" width="350px" />
      </ul>
      <ul class="flex">
        <Field
          title="Nome Fantasia"
          :data="data['NOME FANTASIA']"
          width="350px"
        />
        <Field
          title="Razão social"
          :data="data['RAZAO SOCIAL']"
          width="350px"
        />
      </ul>


      <ul class="flex">
        <Field
          title="CNAE"
          :data="data['CNAE PRINCIPAL CODIGO']"
          width="220px"
        />
        <Field
          title="Descrição"
          :data="data['CNAE PRINCIPAL DESCRICAO']"
          width="350px"
        />
      </ul>

      <ul class="flex">
        <Field
          title="CEP"
          :data="data['CEP']"
          :mask="['#####-###']"
          width="220px"
        />
        <Field
          title="Endereço"
          :data="data['TIPO LOGRADOURO'] + ' ' + data['LOGRADOURO']"
          width="350px"
        />
        <Field title="Nº" :data="data['NUMERO']" width="350px" />
      </ul>
      <ul class="flex">
        <Field title="Compl" :data="data['COMPLEMENTO']" width="220px" />
        <Field title="Bairro" :data="data['BAIRRO']" width="350px" />
        <Field title="Cidade" :data="data['MUNICIPIO'] + '-' + data['UF']" width="350px"/>
      </ul>

      <ul class="flex">
        <Field
          title="Telefone"
          :data="data['DDD'] + data['TELEFONE']"
          :mask="['(##) #####-####']"
          width="220px"
        />
        <Field title="Email" :data="data['EMAIL']" width="350px" />
      </ul>
    </div>
    <button @click="newQuery">Nova consulta</button>
  </div>
</template>

<script>
import Field from "./Field.vue";
import { mask } from "vue-the-mask";
export default {
  directives: { mask },
  components: { Field },
  methods: {
    newQuery () {this.$emit('newQuery')}
  },
  name: "CnpjDetails",
  props: {
    data: Object,
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.container h1 {
  color: rgb(255, 255, 255);
  text-shadow: 5px 10px 20px rgba(75, 37, 1, 0.37);

}
.data{
  padding: 40px 50px;
  border-radius: 8px;
  width: 60%;
  display: flex;
  flex-direction: column;
  background-color: white;
  box-shadow: 5px 5px 100px rgba(75, 37, 1, 0.233);
}
.data ul {
  display:flex;
}
.container h1 {
  padding: 50px;
  font-size: 4rem;
}
.container button { 
  margin-top: 16px;
  padding: 12px 30px;
  font-size: 16px;
  font-weight: 600;
}
</style>
