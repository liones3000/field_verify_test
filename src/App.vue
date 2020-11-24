<template>
  <div id="app">
    <div class="container">
      <h1>Card validate</h1>
      <Form :valid-card="validCard" @notifyMsg="notifyHandler" />
      <Notify :notify="notifyMsg" />
    </div>
  </div>
</template>

<script>
import Form from "./components/form";
import Notify from "./components/notify";

export default {
  name: "App",
  components: {
    Form,
    Notify
  },
  data: () => ({
    notifyMsg: null,
    validCard: {
      card_number: "2020-2020-2020-2020",
      exp_date: "12-20",
      card_cvv: "202"
    }
  }),
  methods: {
    notifyHandler(type) {
      this.notifyMsg = type;
    }
  }
};
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 30px;
  .container {
    max-width: 700px;
  }
}
</style>
