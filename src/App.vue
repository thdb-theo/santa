<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/santa-claus.svg" width="150px" />
    <Santa msg="Welcome to Secret Santa!" />
    <santa-form @person-added="addPerson"></santa-form>
    <ul id="santalist">
      <li v-for="person in Santas" :key="person.name">
        {{ person.name }}
      </li>
    </ul>
  </div>
</template>

<script>
import Santa from "./components/Santa.vue";
import SantaForm from "./components/SantaForm.vue";

export default {
  name: "App",
  components: {
    Santa,
    SantaForm,
  },
  data() {
    return {
      Santas: [],
    };
  },
  methods: {
    addPerson(person) {
      this.Santas.push({ name: person });
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

#santalist {
  min-height: 5cm;
  width: 50%;
  margin: auto;
  margin-top: 20px;
  padding-top: 15px;
  padding-bottom: 15px;
  /* border-style: solid;
  border-color: #e40a2d;
  border-width: 2px; */
}
ul {
  text-align: center;
  list-style: none;
  padding: 0;
}
</style>
