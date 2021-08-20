<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png" width="25%" />
    <h1>Champion Search</h1>
    <textarea
      v-model="query"
      height="100"
      rows="20"
      cols="80"
      name="comment"
      form="usrform"
    >
Enter text here...</textarea
    >
    <p>
      {{ filteredList.match(/,/g).length + " Skin(s)" }}
    </p>
    <p>
      {{ filteredList }}
    </p>
  </div>
</template>

<script>
import states from "./skins.json";

export default {
  name: "App",
  data: () => ({
    skinList: "",
    query: "",
  }),
  computed: {
    filteredList: function () {
      const querys = this.query.split("\n");
      const champions = states.filter((skin) => {
        return querys.includes(skin.name);
      });
      const lastFromArray = champions[champions.length - 1];
      let finalArray = "[";
      for (const champion of champions) {
        finalArray += "'" + champion.id;
        if (champion !== lastFromArray) {
          finalArray += "',";
        }
      }
      finalArray += "']";
      return finalArray;
    },
  },
  mounted() {
    this.query = `Conqueror Jax
Conqueror Jax Prestige Edition
DWG Jhin
DWG Kennen
DWG Leona
DWG Nidalee
DWG Twisted Fate`;
  },
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
