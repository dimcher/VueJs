<template>
    <div class="actions">
        <button  @click="actionOption">NEW</button>
        <button :disabled="1">SAVE</button>
        <button :disabled="1">DELETE</button>
    </div>
</template>

<script>
export default {
    name: 'Actions',
    props: {
    },
    methods: {
        actionOption: function () {
            this.$emit('doAction', { type: 'NEW' });
        }
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .actions {
    text-align: center;
  }
  .actions button {
      margin: 3px;
  }
</style>
