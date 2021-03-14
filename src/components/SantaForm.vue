<template>
  <form @submit.prevent="onSubmit">
    <label for="new-person-input"></label>
    <input
      type="text"
      id="new-person-input"
      name="new-person"
      autocomplete="off"
      v-model="name"
      placeholder="Santa's name"
      cen
    />
    <input
      type="email"
      id="new-email-input"
      name="new-email"
      autocomplete="off"
      v-model="email"
      placeholder="Santa's e-mail address"
      cen
    />
    <input type="submit" value="Add">
  </form>
</template>

<script>
export default {
  methods: {
    onSubmit() {
      this.$emit("person-added", this.name, this.email);
      this.name = "";
      this.email = ""
    },
  },
  data() {
    return {
      name: "",
      email: "",
    };
  },
};
</script>

<style scoped>
input {
    margin: 0px 5px;
    border-radius: 10px;
    border: thin solid #999;
    height: 20px;
    text-align: center;
}

input[type="submit"]{
  cursor:pointer;
  height:25px;
}

input[type="text"], input[type="email"], textarea, select { 
    outline: none;
}


input[type="submit"]:hover {
  letter-spacing: 1px;
  box-shadow: 2px 2px #bbb;
}
</style>