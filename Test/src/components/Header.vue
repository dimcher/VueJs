<template>
  <div class="header">
    <Accounts :account="account" :googleId="googleId" @getAccount="getAccount($event)" />
    <Actions />
  </div>
</template>

<script>
import Accounts from './Accounts'
import Actions from './Actions'

export default {
  name: 'Header',
  data: () => {
    return {
    }
  },
  props: {
      'account': {
          type: String
      },
      googleId: {
          style: String
      }
  },
  components: {
    Accounts,
    Actions
  },
  methods: {
    getAccount: function (event) {
      this.$emit('getAccount', event);
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .header {
    display: flex;
    justify-content: space-between;
    align-items: left;
  }
</style>
