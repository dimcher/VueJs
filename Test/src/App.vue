<template>
  <div id="app">
    <div v-if="googleId">
      <Header :account="account" :googleId="googleId" @getAccount="getAccount($event)" @doAction="doAction" />
      <Table :account="account" :googleId="googleId" :toDo="action" />
    </div>
    <div v-else>
      <GoogleId @getGoogleId="getGoogleId" />
    </div>
  </div>
</template>

<script>
import Table from './components/Table'
import Header from './components/Header'
import GoogleId from './components/GoogleId'

export default {
  name: 'App',
  components: {
    Header,
    Table,
    GoogleId,
  },
  props: {
      googleIds: {
        style: String,
        default: ""
      }
  },
  data: () => {
    return {
      account: "1",
      googleId: "",
      action: {}
    }
  },
  methods: {
    getGoogleId: function (id) {
      this.googleId = id;
    },
    getAccount: function (account) {
      this.account = account;
    },
    doAction: function (action) {
        this.action = action;
    }
  }
}
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
