<template>
  <div id="app">
    <Header :account="account" :googleId="googleId" @getAccount="getAccount($event)" />
    <Table :account="account" :googleId="googleId" />
  </div>
</template>

<script>
import Header from './components/Header'
import Table from './components/Table'

export default {
  name: 'App',
  components: {
    Header,
    Table
  },
  props: {
      googleId: {
        style: String,
        default: '81c14de2-6891-461b-9ea6-3ed218675b8f'
      }
  },
  data: () => {
    return {
      account: "1"
    }
  },
  methods: {
    getAccount: function (event) {
      this.account = event;
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
