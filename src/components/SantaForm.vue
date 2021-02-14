<template>
  <form @submit.prevent="onSubmit">
    <label for="new-person-input"></label>
    <input
      type="text"
      id="new-person-input"
      name="new-person"
      autocomplete="off"
      v-model="name"
      placeholder="Add a santa here"
      cen
    />
    <button type="submit">Add</button>
  </form>
</template>

<script>
export default {
  methods: {
    onSubmit() {
      this.$emit("person-added", this.name);
      this.name = "";
    },
  },
  data() {
    return {
      name: "",
    };
  },
};
</script>

<style>
input {
    text-align: center;
}
</style>