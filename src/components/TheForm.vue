<template>
  <form @submit.prevent="FormHandler">
    <input type="text" placeholder="Income description..." v-model="formData.desc">
    <input type="number" placeholder="Income value..." v-model="formData.value">
    <input type="data" placeholder="Income date..." v-model="formData.date">
    <input type="submit" value="SUBMIT">
  </form>
</template>

<script>
import { reactive } from 'vue';
export default {
  props: {
    state: Object,
  },
  setup (props, {emit}) {
    const formData = reactive({
      desc: null,
      value: null,
      date: null,
    });

    function FormHandler() {
      emit("add-income", {
        desc: formData.desc,
        value: formData.value,
        date: formData.date
      });


      formData.desc.desc = null;
      formData.value = null;
      formData.data = null;
    }
    return {
      FormHandler,
      formData
    }
  }
}
</script>


<style scoped>
form {
  display: flex;
  justify-content: center;
  margin-top: 30px;
}
form input {
  color: #888;
  border: none;
  outline: none;
  font-size: 20px;
}
form input::placeholder {
  color: #AAA;
}
form input:not([type="submit"]) {
  display: block;
  background: #FFF;
  border: none;
  outline: none;
  padding: 5px 15px;
}
form input[type="submit"] {
  display: block;
  background: none;
  border: none;
  outline: none;
  color: #FFF;
  font-weight: 500;
  text-shadow: 0 1px 3px rgba(0, 0, 0, 0.2);
  padding: 5px 15px;
  background-color: #FFCE00;
  cursor: pointer;
}
form input:first-of-type {
  border-radius: 8px 0 0 8px;
}
form input:last-of-type {
  border-radius: 0 8px 8px 0;
}
</style>
