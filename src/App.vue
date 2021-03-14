<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/santa-claus.svg" width="150px" />
    <Santa msg="Welcome to Secret Santa!" />
    <santa-form @person-added="addPerson"></santa-form>
    <table id="santatable">
      <tr v-for="person in Santas" :key="person.name">
        <td class="name">{{ person.name }}</td>
        <td class="email">{{ person.email }}</td>
        <td class="rm"><button type="button" @click="removePerson(person)">🗑</button></td>
      </tr>
    </table>
    <form @submit.prevent="submit">
      <input type="submit" value="Submit" />
    </form>
  </div>
</template>

<script>
import Santa from "./components/Santa.vue";
import SantaForm from "./components/SantaForm.vue";
import emailjs from "emailjs-com";

function shuffle(array) {
  var currentIndex = array.length,
    temporaryValue,
    randomIndex;

  // While there remain elements to shuffle...
  while (0 !== currentIndex) {
    // Pick a remaining element...
    randomIndex = Math.floor(Math.random() * currentIndex);
    currentIndex -= 1;

    // And swap it with the current element.
    temporaryValue = array[currentIndex];
    array[currentIndex] = array[randomIndex];
    array[randomIndex] = temporaryValue;
  }

  return array;
}

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
    addPerson(person, email) {
      this.Santas.push({ name: person, email: email });
    },
    removePerson: function(person) {
      const index = this.Santas.indexOf(person);
      if (index > -1) {
        this.Santas.splice(index, 1);
      }
    },
    submit() {
      shuffle(this.Santas);
      let any_errors = false;
      for (let i = 0; i < this.Santas.length; i++) {
        // we form a line of santas
        // everyone gives to the one after themselves
        const santa = this.Santas[i];
        const recipient = this.Santas[(i + 1) % this.Santas.length];

        var body = {
          to_email: santa.email,
          to_name: santa.name,
          message: recipient.name,
        };
        try {
          emailjs.send(
            "service_0b5m4pv",
            "template_kjfavbi",
            body,
            "user_oloAALczid6FEeLFDEVng"
          );
        } catch (error) {
          any_errors = true;
          console.log({ error });
        }
      }
      if (!any_errors) {
        alert("Emails sent successfully!");
      }
    },
  },
};
</script>

<style scoped>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

table {
  margin: auto;
  margin-top: 20px;
  margin-bottom: 20px;

  border: none;
  border-collapse: collapse;
  border-spacing: 20px 0px;
}

table td {
  height: 30px;
  border-left: thin solid #999;
  border-right: thin solid #999;
}

table td:first-child {
  border-left: none;
}

table td:last-child {
  border-right: none;
}
.name {
  text-align: right;
  padding-right: 10px;
  text-transform: capitalize;
}
.email {
  text-align: center;
  padding-left: 10px;
  padding-right:10px
}
.rm {
  padding-left:10px;
  text-align: left;
}
input[type] {
  border-radius: 10px;
  border: thin solid #999;
  padding: 5px 5px;
  cursor: pointer;
}

button {
  background-color: white;
  border:none;
  cursor:pointer;
  font-size: 15px;
}
input[type]:hover {
  letter-spacing: 1px;
  box-shadow: 2px 2px #bbb;
}
</style>
