<template>
  <div>
    <h1 :key="index" v-for="(msg, index) in msgs">{{ msg }}</h1>
    <div>
      <p>Local data</p>
      <div :key="index" v-for="(jsonlocaldato, index) in jsonlocaldatos">
        <h2>
          Marca: {{ jsonlocaldato.marca }} * Cor: {{ jsonlocaldato.cor }} *
          Modelo: {{ jsonlocaldato.modelo }} * Portas:
          {{ jsonlocaldato.portas }}
        </h2>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import myData from "../assets/datax.json";
export default {
  name: "Main",
  data() {
    return {
      msgs: [],
      jsonlocaldatos: myData,
    };
  },
  methods: {
    getInfoApi() {
      // em rota teremos o problema de cors
      const path = "http://localhost:5000/api/v1/all"; //from flask
      axios
        .get(path)
        .then((res) => {
          this.msgs = res.data.carros;
          console.log(this.msgs);
        })
        .catch((error) => {
          console.log("----> ", error);
        });
    },
  },
  created() {
    this.getInfoApi();
  },
};
</script>

<style>
</style>