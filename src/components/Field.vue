<template>
      <li>
        <label class="field">{{title}}</label>
        <input v-if="mask" type="text" :value="data" disabled v-mask="[...mask]" :style="'width: '+ width"/>
        <input v-else type="text" :value="data" disabled :style="'width: '+ width" />
      </li>
</template>

<script>
import { mask } from 'vue-the-mask'
export default {
  directives: { mask },
  name: 'Field',
  props: {
    title: String,
    data: String,
    mask: Array,
    width: String
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
label{
  font-size: 0.75rem;
  margin-top: 16px;
  color: #888;

}
li {
  display: flex;
  align-items: flex-start;
  flex-direction: column;
}
input {
  font-size: 16px;
  font-weight: bold;
  background-color: transparent;
  border: none;
}
</style>
