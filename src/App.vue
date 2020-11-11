<template>
  <div id="app">
    <div class="list">
      <input type="text" v-model="city" v-on:change="check()" />
      <br />
      <select type="text" style="margin-top: 40px">
        <option
          v-for="address in addresses"
          v-bind:key="address.apiKey"
          value="address.Description"
        >
          {{ address.Description }}
        </option>
      </select>
    </div>
  </div>
</template>

<script>
import Vue from "vue";
export default {
  name: "App",
  data: function () {
    return {
      addresses: [],
      city: "",
    };
  },
  mounted: function () {
    Vue.axios
      .post("https://api.novaposhta.ua/v2.0/json/", {
        modelName: "AddressGeneral",
        calledMethod: "getWarehouses",
        methodProperties: {
          CityName: this.city,
        },
        apiKey: "277a5fd502b9e68b334e76f2056fb077",
      })
      .then((response) => {
        this.addresses = response.data.data;
        console.log(response.data.data);
      });
  },

  methods: {
    check: function () {
      Vue.axios
        .post("https://api.novaposhta.ua/v2.0/json/", {
          modelName: "AddressGeneral",
          calledMethod: "getWarehouses",
          methodProperties: {
            CityName: this.city,
          },
          apiKey: "277a5fd502b9e68b334e76f2056fb077",
        })
        .then((response) => {
          this.addresses = response.data.data;
          console.log(response.data.data);
        });
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
