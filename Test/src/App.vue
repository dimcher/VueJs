<template>
  <div id="app">
    <div v-if="googleId">
      <Header :account="account" :googleId="googleId" @getAccount="getAccount($event)" />
      <Table :account="account" :googleId="googleId" />
    </div>
    <div v-else>
      <GoogleId @getGoogleId="getGoogleId" />
    </div>
  </div>
</template>

<script>
import GoogleId from './components/GoogleId'
import Header from './components/Header'
import Table from './components/Table'

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
        default: ''// 81c14de2-6891-461b-9ea6-3ed218675b8f
      }
  },
  data: () => {
    return {
      account: "1",
      googleId: ""
    }
  },
  methods: {
    getGoogleId: function (id) {
      this.googleId = id;
    },
    getAccount: function (account) {
      this.account = account;
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
