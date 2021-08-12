<template>
    <td><button @click="actionOption">DELETE</button></td>
</template>

<script>
export default {
    name: 'BtnOptionDelete',
    props: {
        option: {
            type: Object
        }
    },
    methods: {
        actionOption: function () {
            this.$emit('doAction', { type: 'DELETE', option: this.option });
        }
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    
</style>
