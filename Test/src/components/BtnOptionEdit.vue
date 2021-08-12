<template>
    <td><button @click="actionOption">EDIT</button></td>
</template>

<script>
export default {
    name: 'BtnOptionEdit',
    props: {
        option: {
            type: Object
        }
    },
    methods: {
        actionOption: function () {
            this.$emit('doAction', { type: 'EDIT', option: this.option });
        }
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    
</style>